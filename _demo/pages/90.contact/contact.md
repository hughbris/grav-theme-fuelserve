---
title: Contact
process:
  twig: true
cache_enable: false

forms:
  contact:
    title: Contact form # TODO: capitalise in Twig
    # action: 
    method: POST
    # classes: 'contact-form agileits-w3layouts'

    fields:
      cols:
        type: columns
        classes: thirds
        fields:
          col1:
            type: column
            fields:
              name:
                type: text
                label: Name
                display_label: false
                placeholder: Name
                validate:
                  required: true

          col2:
            type: column
            fields:
              email:
                type: email
                label: Email
                display_label: false
                placeholder: Email
                validate:
                  required: true

          col3:
            type: column
            fields:
              phone:
                type: tel
                label: Telephone
                display_label: false
                placeholder: Telephone

      message:
        type: textarea
        label: Message
        display_label: false
        placeholder: Message

    buttons:
      submit:
        type: submit
        value: Submit
        classes: 'btn1 btn-1 btn-1b w3-agile'

    process:
      - ip:
        label: User IP Address
      - suppress: [ip] # TODO
      - email:
          from: "{{ config.plugins.email.from }}"
          to: "{{ form.value.email }}"
          to_name: "{{ form.value.name|e }}"
          reply_to: "{{ config.plugins.email.to ?: config.plugins.email.from }}"
          subject: "Thanks for getting in touch"
          body:
            - content_type: 'text/html'
              body: "<html><body>\n<p>Thank you for your message. Here is a copy for your records.</p>{% include 'forms/data.html.twig' with {'suppress': true} %}\n</body></html>"
            - content_type: 'text/plain'
              body: "Thank you for your message. Here is a copy for your records.\n\n{% include 'forms/data.txt.twig' %}"
      - email:
          from: "{{ config.plugins.email.from }}"
          from_name: "{{ form.value.name|e }} via {{ config.plugins.email.from_name}}"
          to: "{{ config.plugins.email.to ?: config.plugins.email.from }}"
          reply_to: "{{ form.value.email }}"
          subject: "Website message received from {{ form.value.name|e }}"
          body:
            - content_type: 'text/html'
              body: "<html><body>\n<p>Here's the details:</p>{% include 'forms/data.html.twig' with {'suppress': true} %}\n</body></html>"
            - content_type: 'text/plain'
              body: "Here's the details:\n\n{% include 'forms/data.txt.twig' %}"
      - save:
          fileprefix: contact-
          dateformat: Ymd-His-u
          extension: txt
          body: "{% include 'forms/data.txt.twig' %}"
      - message: Thanks for getting in touch. You should see a receipt in your inbox. I'll get back to you soon.
      - redirect: contact/thanks

---

#### Miscellaneous Information:

Lorem ipsum dolor sit amet, consectetur adipisicing elit,sheets containing Lorem Ipsum passages, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.It was popularised in the 1960s with the release of Letraset and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
