# Nextflow_Junyong

## Channel

set1
`.fromPath('PATH')` - create a channel emitting one or more file paths by using the `fromPath` method and specifying a path string as an argument.

`.into{name of the copies of the source channel1;name of the copies of the source channel2,...}` - create two (or more) copies of the source channel. Then, use the new channels as input for the processes.

## procsee

### format

process "process name"{
  your setting
  script:
  """
  your script
  """
}

#### input

format

input : file "name_of_parameter" from "name of channel"

then use $name_of_parameter in script
