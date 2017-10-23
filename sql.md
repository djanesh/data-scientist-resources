It sets how the database server sorts. in this case:

SQL_Latin1_General_CP1_CI_AS
breaks up into interesting parts:

* latin1 makes the server treat strings using charset latin 1, basically ascii
* CP1 stands for Code Page 1252
* CI case insensitive comparisons so 'ABC' would equal 'abc'
* AS accent sensitive, so 'ü' does not equal 'u'
P.S. For more detailed information be sure to read @solomon-rutzky's answer.
