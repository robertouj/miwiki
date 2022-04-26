---
title: React - Codes (long)
description: 
published: true
date: 2022-04-06T08:42:01.210Z
tags: 
editor: markdown
dateCreated: 2022-04-04T18:51:50.322Z
---

# Codes (long)

Here some longer codes in React.

## Modal

Create a hook to manage the states.

```js
import { useState } from "react";

const useModal = (initialValue = false) => {
  const [isOpenModal, setIsOpenModal] = useState(initialValue);

  const toggleModal = () => setIsOpenModal(!isOpenModal);

  return [isOpenModal, toggleModal];
};

export default useModal;
```

The Modal component containing a children to create the content.

```jsx
import React from "react";
import "./Modal.css";

const Modal = ({ isOpen, toggleModal, title, children }) => {
  const handleModalDialogClick = (e) => {
    e.stopPropagation();
  };

  return (
    <div className={`modal ${isOpen && "modal-open"}`} onClick={toggleModal}>
      <div className="modal__dialog" onClick={handleModalDialogClick}>
        <h1>{title}</h1>
        <button onClick={toggleModal}>Close Modal</button>

        {children}
      </div>
    </div>
  );
};

export default Modal;
```

The css.

```css
.modal {
  background-color: rgba(0, 0, 0, 0.85);
  width: 100vw;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 9999;
  display: none;
  justify-content: center;
  align-items: center;
}

.modal__dialog {
  background: #ddd;
  padding: 10px;
  width: 300px;
  height: 400px;
}

.modal-open {
  display: grid;
}
```

Controling the modal in the app.

```jsx
import React from "react";
import Modal from "./components/Modal";
import useModal from "./hooks/useModal";

function App() {
  const [isOpenLoginModal, toggleLoginModal] = useModal(false);

  return (
    <div>
      <button onClick={toggleLoginModal}>Open Login Modal</button>

      <Modal
        isOpen={isOpenLoginModal}
        toggleModal={toggleLoginModal}
        title="Login"
      >
        <form>
          <input type="email" placeholder="Correo" />
          <input type="password" placeholder="Contraseña" />
        </form>
      </Modal>
  );
}

export default App;
```

## ToDo List

This code is an example how to use an advanced Form with add, edit, cancel and control messages.

- This code uses React Bootstrap for the components and other css properties.

```jsx
import React, { useEffect, useState } from "react";
import { Form, Button, Alert } from "react-bootstrap";

const initialFormValues = {
  title: "",
  description: "",
};

const TodoForm = ({ todoAdd, todoEdit, setTodoEdit, todoUpdate }) => {
  const [formValues, setFormValues] = useState(initialFormValues);
  const { title, description } = formValues;
  const [errorMessage, setErrorMessage] = useState(null);
  const [successMessage, setSuccessMessage] = useState(null);

  useEffect(() => {
    if (todoEdit) {
      setFormValues(todoEdit);
      setErrorMessage(null);
    }
  }, [todoEdit]);

  const handleInputChange = (e) =>
    setFormValues({
      ...formValues,
      [e.target.name]: e.target.value,
    });

  const handleAddButton = () => {
    if (title.trim() === "") {
      setErrorMessage("Title can't be empty.");
      return;
    }

    if (description.trim() === "") {
      setErrorMessage("Description can't be empty.");
      return;
    }

    !todoEdit ? todoAdd(formValues) : todoUpdate(formValues);
    setTodoEdit(null);
    setFormValues(initialFormValues);
    setSuccesslMessage(`Task ${!todoEdit ? "added" : "edited"} successfuly`);
    setTimeout(() => {
      setSuccessMessage(null);
      setErrorMessage(null);
    }, 4000);
  };

  const handleCancelButton = () => {
    setTodoEdit(null);
    setFormValues(initialFormValues);
    setErrorMessage(null);
  };

  return (
    <div>
      <h2 className="text-center display-6">
        {todoEdit ? "Edit" : "New"} Task
      </h2>
      {errorMessage && <Alert variant="danger">{errorMessage}</Alert>}
      {successMessage && <Alert variant="success">{successMessage}</Alert>}
      <form>
        <Form.Control
          type="text"
          placeholder="Title"
          value={title}
          name="title"
          onChange={handleInputChange}
        />
        <Form.Control
          as="textarea"
          placeholder="Description"
          rows={3}
          className="mt-2"
          value={description}
          name="description"
          onChange={handleInputChange}
        />
        <div className="d-grid">
          <Button
            size="block"
            variant="primary"
            className="mt-2"
            onClick={handleAddButton}
          >
            {todoEdit ? "Edit" : "Add"} Task
          </Button>
          {todoEdit ? (
            <Button
              size="block"
              variant="warning"
              className="mt-2"
              onClick={handleCancelButton}
            >
              Cancel edition
            </Button>
          ) : (
            ""
          )}
        </div>
      </form>
    </div>
  );
};

export default TodoForm;
```