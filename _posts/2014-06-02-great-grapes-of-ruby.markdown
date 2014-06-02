
[Grape][grape] is a ruby microframework for developing API web-applications.

By removing view logic and other features not required for an API, it achives great performance, with simple, modular and easy to read code.

[Grape][grape] has a number of built in methods which allow the easy creation of an API based on a DSL.

Here's an example API which which provide a JSON response `{"acknowledged": true}` to a URL `/ping`.

~~~~ruby

require 'grape'
class MyAPI < Grape::API
    format :json # Instruct Grape to return JSON formatted objects
    
    get '/ping' do
      {acknowledged: true}
    end
end

~~~~

Note that that the method itself has only two statements. A call to `get` with a path `/ping` and a block which has the other statement.
The other statement is the return value. Simple!


What about parameter input, and validation? Grape has you covered!

NOTE: this example omits the class declaration and `format`, giving only the API method.

~~~~ruby

  params do
    requires :message , type: String , desc: "Message to reply with"
  end
  
  get '/echo' do
    {message: params[:message]}
  end
~~~~

This example uses a request parameter "message" which could be provided either in a query string `?message=Hello`
or in the request body.

Grape also supports positional path parameters much like rails. The `params block is the same as before.

~~~~ruby
  get '/echo/:message' do
    {message: params[:message]}
  end
~~~~

[grape]: http://intridea.github.io/grape/
