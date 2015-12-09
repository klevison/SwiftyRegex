# SwiftyRegex

SwiftyRegex is a regular expression matcher based on the pcre2 library

## License

SwiftyRegex is licensed under the BSD 3 Clause license. See LICENSE.txt for full license text.

## Dependencies

SwiftyRegex needs the pcre2 library installed in `/usr/local`.

On a Mac just use Homebrew:

~~~bash
brew install pcre2
~~~

Linux support is planned but not tested

## Usage

Instanciate a `RegEx` object and call the `match` function:

~~~swift
import SwiftyRegex

do {
    let re = try RegEx(pattern: "([0-9]+)[\\s]*:[\\s]*(?P<text>.*)")
    let matches = re.match("1234 : Hello World")

    let numbered = matches.numberedParams
    let named = matches.namedParams
    
    // numbered.count == 3
    // numbered[1] == "1234"
    // numbered[2] == "Hello World"

	// named.count == 1
	// named["text"] == "Hello World"

} catch RegEx.Error.InvalidPattern(let offset, let message) {
	print("Pattern invalid @ \(offset): \(message)")
} catch {
	// should not be reached ever
}
~~~

The initializer stores the compiled pattern, so keep the `RegEx` object if you want to do multiple matches.