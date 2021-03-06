# checklist-model
AngularJS directive for list of checkboxes

## Why this is needed?  
In Angular one checkbox `<input type="checkbox" ng-model="...">` is linked 
with one model.  
But in practice we usually want one model to store array of checked values 
from several checkboxes.  
**Checklist-model** solves that task without additional code in controller.   
You should play with attributes of `<input>` tag:
  
| Attribute          | Mandatory | Description                                   |
| :----------------: | :-------: | --------------------------------------------- |
| `checklist-model`  | Yes       | Use instead of `ng-model`                     |
| `checklist-value`  | No        | What should be picked as array item           |
| `value`            | No        | What should be picked as item, but unlike `checklist-value`, this does not evaluate as an angular expression, but rather a static value |
| `ng-model`         | No        | Every checkbok will span a new scope and define a variable named `checked` to hold its state. You can modify this name by using this attribute. |
| `checklist-comparator` | No   | A custom comparator. If it starts with dot(`.`) then it will be an expression applied to the array item. Otherwise it should evaluate to a function as an angular expression. The function return true if the first two arguments are equal and false otherwise. |
| `checklist-change` | No       | An angular expression evaluated each time the `checklist-model` has changed. |

* If you modify directly the value of the `checklist-model`, it is possible that the UI won't be updated. This is because this directive looks for the model in the parent, not in the current scope. Instead of doing `checklistModelList = []` it is better to do `checklistModelList.splice(0, checklistModelList.length)` or wrap it in another object.
* If you're using `track by` you must specify the same thing for `checklist-value` too. See [#46](https://github.com/vitalets/checklist-model/issues/46).

Please, try out
* live demo: http://vitalets.github.io/checklist-model
* Jsfiddle: http://jsfiddle.net/Ebv3p/2/  
* Plunkr example (more advanced): http://plnkr.co/edit/pZLF0KesMDnIap0eCfSG?p=preview
* Plunkr example for [tree list](http://plnkr.co/edit/QPLk98pCljp8dFtptSYz?p=preview)

## Installation
1. Download [latest release](https://github.com/vitalets/checklist-model/releases) or use bower `bower install checklist-model` or install from npm `npm install checklist-model`
2. Add to app dependencies:
````js
var app = angular.module("app", ["checklist-model"]);
````

## How to get support
* Ask a question on StackOverflow and tag it with [checklist-model](http://stackoverflow.com/questions/tagged/checklist-model).
* [Fill in](https://github.com/vitalets/checklist-model/issues/new) an issue.

## Development
We're using grunt as the build system. `grunt jade` generates the demo file and `grunt server` starts the demo server that can be access at `http://localhost:8000`. Tests can be ran by accessing `http://localhost:8000/test`.

The best way to involve is to report an issue/enhancement and then provide a pull request for it using Github usual features.

### How to add a new test case
1. Create a new folder under `docs/blocks` named `your-test`.
2. Create under that folder `ctrl.js` to describe the test Angular controller, `view.html` to describe the view part in HTML and `test.js` for the Angular scenario test. You can use an existing test as an example.
3. Add a line like `- items.push({id: 'your-test', text: 'Your test, ctrlName: 'CtrlTestName', testValue: 'selectedItems'})` to `docs/index.jade`
4. Add a line like `<script src="../docs/blocks/your-test/test.js"></script>` to `test\index.html`
5. Run `grunt jade` to generate `index.html` from `docs/index.jade`
6. Run `grunt server`
7. Access `http://localhost:8000` for samples and `http://localhost:8000/test` for running the tests.

## License
MIT 
