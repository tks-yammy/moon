# Command
## use embulk
### Generate template file. (seed.yml)
<pre><code>
embulk example .
</code></pre>

### Create sample.yml.
<pre><code>
cp -p seed.yml sample.yml
</pre></code>

<pre><code>
# sample.yml
in:
  type: file
  path_prefix: '/opt/embulk/sql.tsv'
out:
  type: stdout
</code></pre>

### Gererate config.yml.
<pre><code>
embulk guess sample.yml -o config.yml
</code></pre>

<pre><code>
# config.yml 
in:
  type: file
  path_prefix: '/opt/embulk/sql.tsv'
out:
  type: stdout
root@embulk:/opt/embulk# cat config.yml 
in:
  type: file
  path_prefix: /opt/embulk/sql.tsv
  parser:
    charset: UTF-8
    newline: LF
    type: csv
    delimiter: "\t"
    quote: '"'
    escape: '"'
    trim_if_not_quoted: false
    skip_header_lines: 0
    allow_extra_columns: false
    allow_optional_columns: false
    columns:
    - {name: c0, type: timestamp, format: '%Y-%m-%d %H:%M:%S'}
    - {name: c1, type: string}
out: {type: stdout}
</code></pre>

### Edit columns name, out section for elasticsearch.
<pre><code>
# config.yml 
in:
  type: file
  path_prefix: /opt/embulk/sql.tsv
  parser:
    charset: UTF-8
    newline: LF
    type: csv
    delimiter: "\t"
    quote: '"'
    escape: '"'
    trim_if_not_quoted: false
    skip_header_lines: 0
    allow_extra_columns: false
    allow_optional_columns: false
    columns:
    - {name: start_time, type: timestamp, format: '%Y-%m-%d %H:%M:%S'}
    - {name: sql_text, type: string}
out: 
  type: elasticsearch
  index: embulk
  index_type: embulk
  nodes:
  - {host: hostname or ip-address}
</code></pre>

# History
2018.09.19 add sample embulk files.

