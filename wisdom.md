# Coding Wisdom

Unstructured notes from different authors.

## Naming

### Classes

- look at what its objects will encapsulate and come up with a name for this group
- *name by what it is, not by what it does*
	- He is a *pixel*, and he can change his color.
	- He is a *file*, and can read his contents from disk.
	- He is an *HTML* document, and he can be rendered.
	- He is a *list* and, and he can pick an element by number.
- `Cash, Target, EncodedText, DecodedData, Content, SortedLines, ValidPage, Source,...`

### Methods

*Elegant Objects Vol. 1 - Yegor Bugayenko*, p. 53, Ch. 2.4
Either builders or manipulators:

- **builders**
	- returns a value
	- is a noun
	- if it returns a boolean use an **adjective**

```typescript
// do
function stream(url: URL): InputStream;
function content(file: File): string;
function sum(a: number, b: number): number;
list.empty();     // is empty
total.negative(); // is negative
file.readable();  // is readable

// don't
function load(url: URL): InputStream;
function read(file: File): string;
function add(a: number, b: number): number;
```

- **manipulators**
	- no return value
	- is a verb

```typescript
class Pixel {
	paint(color: Color): void;
}
const center: Pixel = new Pixel(50, 50);
center.paint(new Color("red"));
```

- if you don't know where to put some peace of code, pick the trivial/obvious place what comes to mind first

## Try New Things/Settings

- give yourself 30 min max, then move on, try on next day or hours later

## Debugging / When Stuck

- give yourself 30 mins, then make a break, switch topics
- check
	- missing closing parenthesis in strings
	- for typos
	- missing backticks, quotes, double quotes
	- if code is generated and regenerate
	- if generated code was edited

## Reviews

Signals from juniors:

- "You are way too much of a perfectionist man"
- "I mean its a little frustrating I will admit but its fine"

## Allan Holub

- _C. Cellular Automata_: Note that it would have been a waste of time to start with the static model. You need to understand the message flow before you can understand the relationships between classes.
- _C. Getters and Setters are Evil:_ if the messaging system is designed carefully (I’ll talk about how in a moment), then you can probably dispense with the get/set methods entirely and make your classes more maintainable as a consequence.

## OO Design

Quality Check

- Can you make massive changes to a class definition—even throw out the whole thing and replace it with a completely different implementation—without impacting any of the code that uses objects of that class?

Design

- If you go through a design process, as compared to just coding, you’ll find that there will be hardly any accessors in your program. The process is important.
- Don’t ask for the information that you need to do some work; ask the object that has the information to do the work for you. Example:

```
// WRONG
Money a, b, c;
//...
a.setValue( a.getValue() + b.getValue() );

// CORRECT
Money a, b, c;
//...
a.increaseBy( b );
```

- Prefer coarse-grained methods because they simplify the code and eliminate the need for most getter and setter methods.
- By designing carefully, focusing on what you need to do rather than how you’ll do it, you’ll eliminate the vast majority of getter/setter methods in your program.
