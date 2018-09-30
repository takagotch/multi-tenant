### multi-tenaut ActiveRecord
---

#### activerecord-multi-renaut
.rb 
https://github.com/citusdata/activerecord-multi-tenant


.php
https://github.com/hyn/multi-tenant

```sh
gem 'activerecord-multi-tenant'
```

```ruby
class PageView < ActiveRecord::Base
  multi_tenant :customer
  belongs_to :site
end
class Site < ActiveRecord::Base
  multi_tenant :customer
  has_many :page_views
end

customer = Customer.find(session[:current_customer_id])
MultiTenant.with(customer) do
  site = Site.find(params[:site_id])
  site.update! last_accessed_at: Time.now
  site.page_views.count
end

class ApplicationController < ActionController::Base
  set_current_tenant_through_filter
  before_action :set_customer_as_tenant
  def set_customer_as_tenant
    customer = Customer.find(session[:current_customer_id])
    set_current_tenant(customer)
  end
end


MultiTenant.enable_write_only_mode


```

