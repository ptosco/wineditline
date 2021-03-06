# WinEditLine

An EditLine API implementation for the native Windows Console.

This BSD-licensed library provides command line editing and history
functions similar to those found in GNU Readline.

Paolo Tosco (*)

*) e-mail: paolo.tosco.mail@gmail.com

http://mingweditline.sourceforge.net/


WinEditLine (formerly MinGWEditLine) is a BSD-licensed, open-source
software aimed at implementing most of the functionality of the GNU
Readline library in the framework of the native Windows Console.
In particular, the following functions have been implemented in the
WinEditLine API:

```
void source_editrc()
char *readline(char *prompt)
char **rl_completion_matches(const char *text,
    char *entry_func(const char *, int))
char *rl_filename_completion_function(const char *text, int state)
void rl_free(void *mem)
int using_history()
void free_history()
void free_history_entry(HIST_ENTRY *entry)
void clear_history()
char *add_history(char *line)
HIST_ENTRY *remove_history(int i)
HIST_ENTRY *replace_history_entry(int i, char *line,
    histdata_t dummy)
HIST_ENTRY **history_list()
int where_history()
int history_length()
HIST_ENTRY *current_history()
HIST_ENTRY *history_get(int offset)
int history_set_pos(int i)
HIST_ENTRY *previous_history()
HIST_ENTRY *next_history()
int read_history(const char *filename)
int write_history(const char *filename)
int append_history(int nelements, const char *filename)
int history_truncate_file(const char *filename, int nlines)
```

Please refer to the website and to the fully commented source code
for more detailed and up-to-date information.

For WinEditLine I have used an icon originally drawn by Mattahan,
which is licensed under the Creative Commons license.
