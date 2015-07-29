# myFirstGolangApp
This is  my first web application by Go lang and How can deploy Go apps to Heroku.

In order to deploy to Heroku you’ll need a Heroku user account. <a href="https://api.heroku.com/signup" target="_blank">Signup is free and instant</a>

You’ll also need a Heroku command-line client. Get it by installing the <a href="https://toolbelt.heroku.com/" target="_blank">Heroku Toolbelt</a> if you haven’t already.

If this is your first time using Heroku, login and upload your SSH key:

<pre>
  $ heroku login
  Enter your Heroku credentials.
  Email: you@example.com
  Password:
  Uploading ssh public key /Users/you/.ssh/id_rsa.pub
</pre>

With that in place, let’s prepare our app for deploying to Heroku.

<b>Git, Procfile, and Godep</b>

In order to deploy to Heroku we’ll need the app stored in Git:

<pre>
  $ git init
  $ git add -A .
  $ git commit -m "Your messages"
</pre>

We’ll also need a Procfile to tell Heroku what command to run for the web process in our app:

<pre>
  $ echo 'web: myFirstGolangApp' > Procfile
</pre>

The recommended way to manage Go package dependencies on Heroku is with <a href="href="https://github.com/kr/godep"", target="_blank">Godep</a>, which helps build applications reproducibly.

Install Godep:

<pre> $ go get github.com/kr/godep</pre>
Now save your dependencies:

<pre> $ godep save </pre>

Add these new files to git again with these commands:

<pre>
  $ git add -A .
  $ git commit -m "Your messages."
</pre>


Now we’re ready to deploy this to Heroku.

Create a new Heroku app, telling it to use the <a href="https://github.com/kr/heroku-buildpack-go.git", target="_blank">Go Heroku Buildpack </a> to build your Go code:

<pre>$ heroku create -b https://github.com/kr/heroku-buildpack-go.git</pre>

Push the code to Heroku:

<pre>$ git push heroku master</pre>

You will see somethings like that: 

<pre>
  -----> Fetching custom git buildpack... done
  -----> Go app detected
  -----> Installing go1.1.2... done
  -----> Running: godep go install -tags heroku ./...
  -----> Discovering process types
         Procfile declares types -> web
  
  -----> Compressing... done, 1.2MB
  -----> Launching... done, v4
         http://ancient-temple-243.herokuapp.com deployed to Heroku
</pre>


Your app should be up and running. Visit it with:

<pre> $ heroku open </pre>

If everything went OK, you should have 1 web process up:

<pre>
  $ heroku ps
</pre>

You can also check your logs to see watch as requests come in:

<pre>
  $ heroku logs --tail
</pre>

That’s it - you now have a running Go app on Heroku!
