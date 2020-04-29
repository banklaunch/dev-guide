---
layout: default
title: "Packages and Class Naming"
date: 2020-04-29
---

### Package naming

public package vs private package
(static check)

- Entity package: **domain**
- DTO package: _ **root** _
- Service Interface package: _ **root** _
- Service Implementation package: **service**
- Controller package: _ **root** _
- Mapper classes: **service**
- Events package: **event**
- EventListener package: \ **\*domain** \*

### Services naming

When do we need interfaces? When do we not need interfaces?

- Interface == api for other modules.

- Use interfaces when other modules use public package of current module

- Internal services should not have interfaces

Interface: _ **CustomerService** _

- Implementation class:

**DefaultCustomerService**

Or depending on context:

MailService -> MailChimpMailService

CaptchaProvider - GoogleCaptchaProvider

~~CustomerServiceImpl~~

~~HeadsCustomerService~~

~~AheadsCustomerService~~

~~BanklaunchCustomerService~~

~~BLCustomerService~~

Overriding default spring beans:

UserDetailsService -\&gt;

~~CustomUserDetailsService~~

~~DefaultUserDetailsService~~

~~HeadsUserDetailsService~~

~~BanklaunchUserDetailsService~~

- Depends on usage:

**BackofficeUserDetailsService**

**InvestorUserDetailsService**

## DTO naming

DTO: BO vs. Core
We always have two DTOs per entity - one for backoffice, one for core module
It is crucial to have both, because sometimes Backoffice models have extra fields joined in queries (_see io.banklaunch.bo.api.loan.NoteModel)_

1. The idea is to ease differentiation of BO Models vs Core Models
   Having
   io.banklaunch.api.investor.account.BankAccountModel
   io.banklaunch.bo.api.bankaccount.BankAccountModel
   We can distinguish them by package, but searching each model class would be easier if we name both model classes differently

| **Core Model**       | **Backoffice Model**   |
| -------------------- | ---------------------- |
| **BankAccount**      | **BankAccountBoModel** |
| ~~BankAccountModel~~ | ~~BankAccountBoModel~~ |
| ~~BankAccountModel~~ | ~~BankAccountDTO~~     |
| ~~BankAccount~~      | ~~BankAccountBoModel~~ |
| ~~BankAccountVO~~    | ~~BankAccountModel~~   |
| ~~BankAccountModel~~ | ~~BankAccountVO~~      |
| ...                  | ...                    |

1. Consistent core modules DTO naming

1. Consistent backoffice module DTO naming
