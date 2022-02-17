## Forms
- The <FormControl> component renders a from control w/Bootstrap styling.
- The <FormGroup> component wraps a from control with proper spacing, along with support for a label, help text, and validation state.
- To ensure accessibility, set controlID on <FormGroup>, and use <FormLabel> for the label.
- The <FormControl> directly renders the <input> or other specified component. 
- For textual form controls, FC adds some additional styles for general appearance, focus state, sizing and more.
- Use Form.File for file inputs. <Form.File id="exampleFormControlFile1" label="Example file input" />

## Sizing 
- Use size on <FormControl> and <FormLabel> to change the size of inputs and labels respectively.
- <Form.Control size="lg" type="text" placeholder="Large text" />

## Readonly
- the readOnly prop on an input prevent modifications of the input's value.
- <Form.Control type="text" placeholder="Readonly input here..." readOnly />

## Layout
- FormControl and FormCheck both apply display: block with width: 100% to controls.
- Additional components and props can be used to vary this layout on a per-form basis.

## Form groups
- The FormGroup component is the easiest way to add some structure to forms.
- Provides a flexible container for grouping of lables, controls, optional help text, and form validation messaging.
- 

## React Bootstrap - Forms
- HTML form element work differently from other DOM elements in React
- Controlled Components - In HTML, form element such as <input>, <textarea>, and <select> typically maintain their own state and update it based on user input. In React, mutable state is typically kept in the state property of components, an donly updated with setState().
- Combine the two making the React state be the "single source of truth"
- React component that renders a form also controls what happens in that form on subsequent user input.
- An input form element whose value is contorlled by React in this way is called a "controlled componenet"
-class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
- Since the value attribute is set on our form element, the displayed value will always be this.state.value, making the React state the source of truth, and since handleChange runs on every keystroke to update the React state, the displayed value will update as the user types.
- With a controlled component, the input's value is always driven by the React state, thus you can now pass the value to other UI element too, or reset it from other event handlers.

## Ttextarea Tag
- In HTML, a <textarea> element defines its text by its children.
- In React, a <textarea> uses a value attribute instead. This way, a form using a <textarea> can be written very similarly to a form that uses a single-line input.
- class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 'Please write an essay about your favorite DOM element.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('An essay was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Essay:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
## Select Tag
- In HTML, <select> creates a drop-down list.
- Instead of React using the selected attribute, uses a value attribute on the root select tag. This is more convenient in a controlled componenet because you only need ot update it in one place.
- class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'coconut'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Your favorite flavor is: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Pick your favorite flavor:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">Grapefruit</option>
            <option value="lime">Lime</option>
            <option value="coconut">Coconut</option>
            <option value="mango">Mango</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}

## File input Tag
- In HTML, an <input type="file"> lets the user choose one or more files from their device storage to be uploaded ot a server or manipulated by JS via the File API.
- Because it's value is read-onluy, it is an uncontrolled component in React.
