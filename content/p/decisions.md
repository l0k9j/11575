csv_trials=trials.csv
title=Decisions
hide_page_title=1

**This is a work in progress**.
To suggest corrections or new entries, please [create a new issue on github](https://github.com/l0k9j/11575/issues).

{% raw %}
<div id="search">

    <h1>Decisions ({{ trials.length }})</h1>

    <label>Filter by keywords: <input type="search" v-model="filter_keywords"></label>
    <br><br>
    <table class="table is-narrow">
        <thead>
            <tr>
                <th>Source</th>
                <th>Company</th>
                <th>Date (D/M/Y)</th>
                <th>Jurisdiction</th>
                <th>Fine</th>
                <th>Press</th>
            </tr>
        </thead>
        <tbody>
            <template v-for="(t, i) in trials"> 
                <tr :class="{'is-striped': i % 2}">
                    <td><a v-if="t.link_verdict" :href="t.link_verdict" target="_blank" v-if="t.authority">Source</a></td>
                    <td>{{ t.company }}</td>
                    <td>{{ t.verdict_date }}</td>
                    <td>{{ t.country }}</td>
                    <td>{{ t.currency }} {{ t.fine|number }}</td>
                    <td><a :href="t.link_article" target="_blank" v-if="t.link_article">article</a></td>
                </tr>
                <tr :class="{'is-striped': i % 2}" v-if="t.summary || t.authority">
                    <td></td>
                    <td colspan="20">
                        <template v-if="t.summary"><strong>Summary: </strong> {{ t.summary }}<br></template>
                        <strong>Authority: </strong>{{t.authority}}
                    </td>
                </tr>
            </template>
        </tbody>
    </table>
</div>
{% endraw %}

<script>

let trials = {{ trials.to_json(orient='table') }}
trials.data = trials.data.sort(
    function(a,b) {
        let diff = (new Date(b.verdict_date_sort) - new Date(a.verdict_date_sort))
        return diff
    }
)
trials.filter_keywords = ''

var app = new Vue({
  el: '#search',
  data: trials,
  filters: {
    number: function (value) {
        if (!value) return ''
        return parseInt(value).toLocaleString()
    }
  },
  computed: {
    trials: function() {
      return this.data.filter(
        t => ((t.company.toLowerCase().indexOf('facebook') > -1) && (t.company + t.country + t.summary + t.authority + t.verdict_date).toLowerCase().indexOf(this.filter_keywords) > -1)
      )
    },
  },
})
</script>
