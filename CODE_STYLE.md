```
// The few text comments we use start with slash, slash, space. Sentences start
// with upper case, periods if multiple sentences, referably wrapped around the
// 80 character column.

// Prefer importing specific lodash functions to keep code size down.
import example from 'lodash/example';

// Snake case identifiers for naming in own code base
const multi_word_name = 'string with single quote delimiters';

const obj = { objects_have: 'sparse spacing' };
const arr = ['arrays', 'have', 'compact', 'spacing'];

const multi_line_obj = {
    multi_line: 'objects',
    have: 'trailing comma',
};
const multi_line_arr = [
    'multi_line',
    'arrays',
    'have',
    'trailing comma',
];

function func() {
    // Statements have space before start of parathesis, function calls do not.
    for (const i = 0; i < 10; i += 1) {
        for (const j = 0; j < 10; j += 1) {
            // Only an innermost single statement block *may* skip curly brackets.
            if (i > j)
                another_func(i, j);
        }
    }

    // (Pretending these are long variable names), prefer wrapping after
    // operators, except trinary which are preferably wrapped before.
    let aaaa, bbbb, cccc;
    const z = aaaa &&
        (bbbb
        ? cccc
        : !cccc);
}

function one_line_func() { return func(); }

// Trailing new line
```
