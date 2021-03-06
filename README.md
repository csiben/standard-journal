# Standard Journal

Standard Journal is a simple blog that's based off your Standard Notes.

![bitario-blog](https://s3.amazonaws.com/bitario/misc/bitario-blog.png)

You publish notes to your blogs via an extension that you add to Standard Notes:

<img src="https://s3.amazonaws.com/bitario/misc/sj-ext.png" width="425"/>

For a live demo, see [bitar.io](https://bitar.io).

Presently, to use this extension, you have to install it on your own server. However, we are exploring making this available as a service that allows us to host a blog for you with just one click.

Installation and configuration is easy.

## Installation

1. Create a file in the config folder called `blog.yml` with the following contents:

	```
	foreground_color: "ffffff"
	background_color: "624dd7"
	title: My Journal
	desc: A journal on technology and startups.
	url: <%= ENV['HOST'] %>
	author_name: Jon Snow
	author_text: by Jon Snow
	author_link: https://twitter.com/winteriscoming
	twitter: https://twitter.com/winteriscoming

	links:
	  - name: Photos
	    url: <%= ENV['HOST'] %>/photos
	  - name: About
	    url: <%= ENV['HOST'] %>/about

	hidden_posts:
	  - photography
	  - about

	```

2. Create a file called `.env` with the following contents:

	```
	SECRET=some secret here
	HOST=http://localhost:3003
	SECRET_KEY_BASE=use "bundle exec rake secret"

	DB_HOST=127.0.0.1
	DB_PORT=3306
	DB_DATABASE=sn_blog
	DB_USERNAME=root
	DB_PASSWORD=
	```

	You should change the contents of this file depending on your environment. If launching to a production environment, use your domain name for host and production database credentials.


2. Create a file in the config folder called `cap.yml` with the following contents:

	```
	default: &default
	  key_path: /path/to/key.pem
	  repo_url: https://github.com/standardnotes/standard-journal.git
	  user: ssh_username

	staging:
	  <<: *default
	  server: staging.yourdomain.com
	  branch: staging
	  deploy_to: ~/standard-journal-staging

	production:
	  <<: *default
	  server: yourdomain.com
	  deploy_to: ~/standard-journal-prod
	```

	Change neccessary values to match your server configuration.

3. Run `bundle install`
4. Run `cap production deploy`

And that's it.

To access your extension from Standard Notes, simply type in your extension's URL, which is `https://yourdomain.com/ext/secret_from_env_file`.

Obviously this is assuming you have an environment set up on your server and a web server that can respond to requests at your domain. This is beyond the scope of this example. However, for general instructions on launching a Ruby server, see [this guide](https://github.com/standardfile/ruby-server/wiki/Deploying-a-private-Standard-File-server-with-Amazon-EC2-and-Nginx).

## License

Licensed under the GPLv3: http://www.gnu.org/licenses/gpl-3.0.html
