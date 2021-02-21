csv_trials=trials.csv

{% raw %}
<div id="search">
    <table class="table is-striped is-narrow">
        <thead>
            <tr>
                <th>Company</th>
                <th>Date</th>
                <th>Country</th>
                <th>Fine</th>
                <th>Summary</th>
                <th>Verdict</th>
                <th>Article</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="t in data">
                <td>{{ t.company }}</td>
                <td>{{ t.verdict_date }}</td>
                <td>{{ t.country }}</td>
                <td>{{ t.fine }}</td>
                <td>{{ t.summary }}</td>
                <td>{{ t.link_verdict }}</td>
                <td>{{ t.link_article }}</td>
            </tr>
        </tbody>
    </table>
</div>
{% endraw %}

<script>
var app = new Vue({
  el: '#search',
  data: {{ trials.to_json(orient='table') }}
})
</script>
