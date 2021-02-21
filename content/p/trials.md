csv_trials=trials.csv

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
{% for i, t in trials.iterrows() %}
<tr>
<td>{{ t.company }}</td>
<td>{{ t.verdict_date }}</td>
<td>{{ t.country }}</td>
<td>{{ t.fine }}</td>
<td>{{ t.summary }}</td>
<td>{{ t.link_verdict }}</td>
<td>{{ t.link_article }}</td>
</tr>
{% endfor %}
</tbody>
</table>
