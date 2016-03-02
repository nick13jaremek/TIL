# Problem

When using the [Paperclip](http://github.com/thoughtbot/paperclip) gem, the uploaded files are accessed through an URL that plainly illustrates the structure of the storage directory.

It would be nice to anonymise such URLs by hashing the file paths.

# Solution
## Based on the steps described on the [Paperclip's Hashing Wiki](https://github.com/thoughtbot/paperclip/wiki/Hashing).

 Override the default `Paperclip` settings by creating a `paperclip_defaults.rb` file in the `config/initializers` directory of your Rails project.

 In order to use a customised path, hash secret and hash digest, use the following configuration override:

````
Paperclip::Attachment.default_options.update({
  :path => ":rails_root/public/system/:class/:attachment/:hash/:style.:extension",
  :hash_digest=>"SHA256",
  :hash_secret => <Some random hash string generated using the SecureRandom.base64(128) command in the Rails console>)
````

 This configuration sets the path to start at the Rails project `public` directory located at the project's root directory.

As for the symbols included in the `path` configuration:
  - `:class` is substituted by the name of the model holding the attachment.
  - `:attachment` is substituted by the name of the attribute that refers to the attached file.
  - `:hash` gets substituted by the hash string generated from the `:hash_secret` using the `:hash_digest`.

 For security purposes, it would be better to store the `:hash_secret` in an environment variable and refer to it using `ENV[VARIABLE_NAME]`.

**Important**

The model containing the attribute for the attached file *must* specify the file path **explicitly** and **matching** the one set in the *Paperclip* configuration file. Otherwise, the attached files download URL will be the default one **which does not include the :hash symbol in its path**.

````
# A model containing an attachment attribute

class Friend < ActiveRecord::Base
  validates :document, attachment_content_type: { content_type: 'application/pdf' }

  ## Here we set the attachment url explicitly
  has_attached_file :document, url: '/system/:class/:attachment/:hash/:style.:extension'
end
````
