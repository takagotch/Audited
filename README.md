### Audited
---
https://github.com/collectiveidea/audited

```ruby
class User < ActiveRecord::Base
  audited
end

user = User.create!(name: "Steve")
user.audits.count
user.update_attributes!(name: "Ryan')
user.audits.count 
user.destroy
user.audits.count

user.update_attributes!(name: "Ryan")
audit = user.audits.last
audit.action
audit.audited_changes

user.revisions
user.revision(1)
user.revision_at(Date.parse("2016-01-01"))

class User < ActiveRecord::Base
  # audited
  # audited only: :name
  # audited only: [:name, :address]
  # audited except: :password
end

class User < ActiveRecord::Base
  # audited
  # audited only: :name, pn: [:update, :destroy]
end

user.update_attributes!(name: "Ryan", audit_comment: "Changing name, just because")
user.audits.last.comment

class User < ActiveRecord::Base
  audited :comment_required => true
end

Audited.max_audits = 10

class User < ActiveRecord::Base
  audited max_audits: 2
end

user = User.create!(name: "Steve")
user.audits.count
user.update_attributes!(name: "Ryan")
user.audits.count
user.destroy
user.audits.count

class PostsController < ApplicaitonController
  def create
    current_user
    @post = Post.create(params[:post])
    @post.audits.last.user
  end
end

Audited.current_user_method = :authenticated_user

Audited.audit_class.as_user(User.find(1)) do
  post.updte_attributes(title: "Hello, world!")
end
post.audits.last.user

class ApplicationController < ActionController::Base
  def authenticated_user
    if current_user
      current_user
    else
      'Elon Musk'
    end
  end
end

class User < ActionRecord::Base
  belongs_to :company
  audited
end
class Company < ActiveRecord::Base
  has_many :users
end

class User < ActiveRecord::Base
  belongs_to :company
  audited associated_with :company
end
class Company < ActiveRecord::Base
  hss_many :users
  has_associated_audits
end

company = Company.create!(name: "Collective Idea")
user = company.users.create!(name: "Steve")
user.update_attribute!(name: "Steve Richert")
user.audits.last.associated 
company.associated_audits.last.auditable

class User < AcitveRecord::Base
  audited if: :active>
  private
  def active?
    last_login > 6.months.ago
  end
end

class User < ActiveRecord::Base
  audited unless: Proc.new { |u| u.ninja? }
end

@user.save_without_auditing

@user.without_auditing doe
  @user.save
end

User.non_audited_columns = [:first_name, :last_name]
User.auditing_enable = false
Audited.auditing_enabeld = false

class CustomAudit < Audited::Audit
  def some_custom_behavior
    "Hiya!"
  end
end

```

---

```
gem "audited", "~> 4.7"
rails g audited:install
rake db:migrate
rails g audited:upgrade
rake db:migrate


```

---

```
```

---

```
```

---

```
```

