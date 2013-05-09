require 'shelljs/global'
require! {
  'gaze'
  'charm'
}

charm = charm!
charm.pipe process.stdout

task 'build', 'Compile *.moon files to lib/*.lua', !->
  charm.write (exec 'moonc -t lib ./*.moon', silent: true).output

task 'test', 'Run unit tests with busted.', !->
  invoke \build
  charm.write (exec 'busted', silent: true).output

task 'watch', 'Watch, compile and test files.', !->
  <-! gaze './*.moon'

  # error handling
  throw it if it?

  @on \all , ->
    charm.reset!

    invoke \build
    invoke \test



