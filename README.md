# Nextflow_Junyong

## impletation

```
./nextflow run filename.nf
```

## Funtion

`.flatten()` - transforms a channel in such a way that every item of type collection or array is flattened so that each single entry is emitted separately by the resulting channel.

ex) file x from foo_ch.flatten()

`.collect()` - collects all the items emitted by a channel to a List and return the resulting object as a sole emission.

`.groupTuple()` - collects tuples (or lists) of values emitted by the source channel grouping together the elements that share the same key. Finally, it emits a new tuple object for each distinct key collected.

`.collectFile()` - gather the items emitted by a channel and save them to one or more files. The operator returns a new channel that emits the collected file. 

script(format)

< $parameter command > save_file

## Channel

### set1(file path)

#### 1. basic
`.fromPath('PATH')`

`.set{name_ch}` - set name of channel

#### 2. connection a source channel to two or more target channels
`.fromPath('PATH')` - create a channel emitting one or more file paths by using the `fromPath` method and specifying a path string as an argument.

`.into{name of the copies of the source channel1;name of the copies of the source channel2,...}` - create two (or more) copies of the source channel. Then, use the new channels as input for the processes.

### set2 (file chunk for spliting)

#### 1. for .txt file

`.fromPath('filename.txt')`

`.splitText()` - split multi-line strings or text file items, emitted by a source channel into chuncks containing n(by) lines, which will be emitted by the resulting channel.

`.set{name_ch}`

argument of splitText

- by: Defines the number of lines in each chunk(default : 1)
- file: Using a string to create split files with a specific name(split index number is autimactically added)

#### 2. for .fa FASTA file

`.fromPath('filename.fa')`

`.splitFasta()` - split the entries emitted by a channel, that are formatted using the FASTA format. It returns a channel which emits a text chunk for each sequence in the received FASTA content

`.set{name_ch}`

argument of splitFasta

- by: Defines the number of sequences in each chunk(default : 1)
- file: Using a string to create split files with a specific name(split index number is autimactically added)

#### 3. for .fastaq FASTQ file

`.fromPath('filename.fastq')`

`.splitFastq()` - split the entries emitted by a channel, that are formatted using the FASTQ format. It returns a channel which emits a text chunk for each sequence in the received item

`.set{name_ch}`

argument of splitFastq

- by: Defines the number of sequences in each chunk(default : 1)
- file: Using a string to create split files with a specific name(split index number is autimactically added)

### set3 (file pairs)

`.fromFilePairs('PATH')` - create a channel emitting the file pairs matching a glob pattern. The pttern must match a common prefix in the paired file names. The matcing files are emitted as tuples in which the first element is the grouping key of the matching pair and the second element is the list of files (sorted in lexicographical order)

-> output : sampleID, file("paramter_name")

`.set {name_ch}`

### set4 (range)

`.from()` - create a channel emitting any sequence of values that are specified as the method argument

argument ex) (1, 3, 5, 7), (0..9) -> (0, 1, 2, 3, 4, 5, 6, 7, 8, 9)

`.map{}` - applies a function of choosgin to every item emitted by a channel, and returns the items so obtained as a new channel. 

ex) {chr -> tuple("sample$chr", file("/some/path/foo.${chr}.indels.vcf"), file("/other/path/foo.snvs.${chr}.vcf"))}

`.set{}`

### set5 (csv)

`.splitCsv()` - pares text items emitted by a channel, that are fromatted using CSV format, and split them into records or group them into list of records with a specified length.

header: true - allow you to referebce eacg value by its name, as shown in the following

by - the number of rows in each chunk

## process
### format

```
process "process name"{
  your setting
  script:
  """
  your command
  """
}
```

### setting

#### format

1 input : 

file "name_parameter" from "name_ch"
  
-> you can use $name_parameter

2 input :

set sampleId, file(reads) from "name_ch"
  
-> you can use $sampleId, $reads





