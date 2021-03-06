# `.update() => Self`

Syncs the enzyme component tree snapshot with the react component tree. Useful to run before checking the render output if something external
may be updating the state of the component somewhere.

NOTE: no matter what instance this is called on, it will always update the root.

NOTE: only updates Enzyme's representation of rendered tree.

NOTE: this does not force a re-render. Use `wrapper.setProps({})` to force a re-render.


#### Returns

`ReactWrapper`: Returns itself.



#### Example

```jsx
class UpdateEnzyme extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0,
    };
    this.increment = this.increment.bind(this);
  }

  increment() {
    const { count } = this.state;
    this.setState({ count: count + 1 });
  }

  render() {
    const { count } = this.state;
    return <button type="button" className="increment" onClick={this.increment}>{count}</button>;
  }
}
```
```jsx
const wrapper = mount(<UpdateEnzyme />);
expect(wrapper.find('button.increment').text()).to.equal('0');
wrapper.instance().increment();

// Update Enzyme's view of output
wrapper.update();

expect(wrapper.find('button.increment').text()).to.equal('1');
```
