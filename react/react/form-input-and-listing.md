# Form Input & Listing the Information

```javascript
import React, { Component } from 'react';

class PhoneBook extends Component {
  state = {
    formState: {
      id: '',
      firstName: '',
      lastName: '',
      email: '',
      mode: 'submit'
    },
    users: [
      {
        id: 0,
        firstName: '',
        lastName: '',
        email: ''
      }
    ]
  };

  resetFormState = () => {
    this.setState({
      formState: {
        firstName: '',
        lastName: '',
        email: '',
        mode: 'submit',
        id: ''
      }
    });
  };

  onChange = event => {
    this.setState({
      formState: {
        ...this.state.formState,
        [event.target.name]: event.target.value
      }
    });
  };

  onSubmit = event => {
    const { users, formState } = this.state;
    event.preventDefault();
    const firstName = event.target.querySelector("input[name='firstName']")
      .value;
    const lastName = event.target.querySelector("input[name='lastName']").value;
    const email = event.target.querySelector("input[name='email']").value;
    if (formState.mode === 'submit') {
      this.setState({
        users: [
          ...this.state.users,
          {
            firstName,
            lastName,
            email,
            id: this.state.users[this.state.users.length - 1].id + 1
          }
        ]
      });
    } else if (formState.mode === 'edit') {
      const index = users.find(user => user.id === formState.id).id;
      users[index] = {
        firstName,
        lastName,
        email,
        id: users[index].id
      };
      this.setState({
        users: [...users]
      });
    }
  };

  updateUser = key => {
    let { users } = this.state;

    this.setState({
      formState: { ...this.state.users[key], mode: 'edit' },
      users
    });
  };

  render() {
    const { users, formState } = this.state;
    return (
      <div>
        <Form
          formState={formState}
          onChange={this.onChange}
          onSubmit={this.onSubmit}
        />
        <Table users={users} />
      </div>
    );
  }
}

const Table = ({ users = [] }) => {
  return (
    <div>
      <div>
        <div>
          <div>First Name</div>
          <div>Last Name</div>
          <div>Email</div>
        </div>
      </div>
      <div>
        {users.map((user, key) => {
          return (
            <div>
              <div>{user.firstName}</div>
              <div>{user.lastName}</div>
              <div>{user.email}</div>
            </div>
          );
        })}
      </div>
    </div>
  );
};

const Field = ({ label = '', name = '', value = '', onChange }) => {
  return (
    <div className="field">
      <label htmlFOR={name}>{label}</label>
      <input type="text" name={name} value={value} onChange={onChange} />
    </div>
  );
};

const Form = ({ formState, onChange, onSubmit }) => {
  return (
    <form className="form" onSubmit={onSubmit}>
      <fieldset>
        <Field
          name="firstName"
          label="user name"
          value={formState.firstName}
          onChange={onChange}
        />
        <Field
          name="lastName"
          label="last name"
          value={formState.lastName}
          onChange={onChange}
        />
        <Field
          name="email"
          label="email"
          value={formState.email}
          onChange={onChange}
        />
      </fieldset>
      <button>{formState.mode}</button>
    </form>
  );
};

export default PhoneBook;
```
