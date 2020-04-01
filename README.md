# Rails Review

For each of the following topics, please answer each of the questions. You can use links and images to support your answer. Once done please make a pull request.

## Has many Through

- [Rails Active Record Intro](https://github.com/sei-entropy/lesson-w11d02-rails-active-record#active-record-associations)
-[Hospital App](https://github.com/sei-entropy/hw-w11d02-rails-hospital)

### Questions

1. What is the role of a join table in a many-to-many relationship?

create another table to but the keys into it .


2. What two columns must be present in a join table?

the silmiler id  and the condithon like when we said 
where doctor.id = patient.doctor_id 


3. Given the example below, edit the code to define a has many :through relationship.

    ```ruby
    class Customer < ActiveRecord::Base
    has_many :products 
    end

    class Product < ActiveRecord::Base
     belongs_to :Customer
    has_many :Purchase 
    end

    class Purchase < ActiveRecord::Base
     belongs_to :Product
    end
    ```


4. Based on #3, give an example of associating two instances via the join model.

SELECT *  FROM Customer 
    INNER JOIN product
        on  customer.id = product.customer_id 



## Devise

- [Devise Lesson](https://github.com/sei-entropy/lesson-w11d03-rails-devise)

### Questions

1. What does the `current_user` method that the Devise gem provides?

current signed-in user


2. What does the `authenticate_user!` method that the Devise gem provides?

To set up a controller with user authentication


3. Write a signout link using the `link_to` rails helper and a devise path.
 ```ruby
<%= link_to 'signout ', destroy_user_session_path, method: :delete %>

```

4. How do I generate a devise model in the terminal?

rails g model Artist name hometown img albums:integer


5. What are the trade offs for using a gem for authentication over a handrolled solution? (no real right answer)




## Validations

- [Validations Lesson](https://github.com/sei-entropy/lesson-w11d03-rails-model-validations)

### Questions

1. Which component, of Rails MVC, is responsible for the business logic?

view 


2. Assume the user's age is an optional field.  Write the validation to verify that a User's age is between 13 and 125 (inclusive).

validates_date :date_of_birth,
:after => Date.new(Date.today.year - 125,
Date.today.month,
Date.today.mday),
:before => Date.new(Date.today.year - 13,
Date.today.month,
Date.today.mday),
:after_message => ‘Birthdate of %s is
invalid’,
:before_message => ‘have to be  more than 13’



3. What would `user.errors.messages` return (for the above User), if you assigned `user.age = 12`?

:before_message => ‘have to be  more than 13’


4. Assume you visit "/customers/new" and enter some invalid information.  Given this controller code, what url would your browser be on after pressing "Create Customer"?

``` ruby
class CustomersController < ApplicationController
  def new
    @customer = Customer.new
  end

  def create
    @customer = Customer.new(customer_params)
    if @customer.save
      redirect_to customer_path(@customer)
    else
      render :new
    end
  end
  ...
  private
  def customer_params
    params.require(:customer).permit(:first_name, :last_name, :age)
  end
end
```


5. Give one reason why we might have the similar validations in the browser, model, and database layer of our application.


