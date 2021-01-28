---
title: Nous contacter
form:
    name: my-nice-form
    fields:
        - name: name
          label: Nom
          placeholder: Votre nom
          autofocus: on
          autocomplete: on
          type: text
          validate:
            required: true

        - name: email
          label: E-mail
          placeholder: Votre adresse e-mail
          type: text
          validate:
            rule: email
            required: true

        - name: message
          label: Message
          size: long
          placeholder: Votre message
          type: textarea
          validate:
            required: true

    buttons:
        - type: submit
          value: Envoyer
          classes: gdlr-button with-border excerpt-read-more

    process:
        - email:
            from: "{{ config.plugins.email.from }}"
            to:
              - "{{ config.plugins.email.from }}"
              - "{{ form.value.email }}"
            subject: "[Feedback] {{ form.value.name|e }}"
            body: "{% include 'forms/data.html.twig' %}"
        - save:
            fileprefix: feedback-
            dateformat: Ymd-His-u
            extension: txt
            body: "{% include 'forms/data.txt.twig' %}"
        - message: Votre message a été envoyé, merci !
        - display: thankyou
---
