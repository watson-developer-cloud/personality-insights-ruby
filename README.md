# Personality Insights Ruby Sinatra Starter Application

## DEPRECATED: this repo is no longer actively maintained. It can still be used as reference, but may contain outdated or unpatched code.

  The IBM Watson [Personality Insights][personality_insights] service uses linguistic analysis to extract cognitive and social characteristics from input text such as email, text messages, tweets, forum posts, and more. By deriving cognitive and social preferences, the service helps users to understand, connect to, and communicate with other people on a more personalized level.

Give it a try! Click the button below to fork into IBM DevOps Services and deploy your own copy of this application on Bluemix.

[![Deploy to Bluemix](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/watson-developer-cloud/personality-insights-ruby)

## Getting Started

1. Create a Bluemix Account

  [Sign up][sign_up] in Bluemix, or use an existing account. Watson Services in Beta are free to use.

2. Download and install the [Cloud-foundry CLI][cloud_foundry] tool

3. Edit the `manifest.yml` file and change the `<application-name>` to something unique.
  ```none
  applications:
  - services:
    - personality-insights-service
    name: <application-name>
    path: .
    memory: 256M

  ```
  The name you use will determinate your application url initially, e.g. `<application-name>.mybluemix.net`.

4. Connect to Bluemix in the command line tool
  ```sh
  $ cf api https://api.ng.bluemix.net
  $ cf login -u <your user ID>
  ```

5. Create the Personality Insights service in Bluemix
  ```sh
  $ cf create-service personality_insights tiered personality-insights-service
  ```

6. Push it live!
  ```sh
  $ cf push <application-name>
  ```

See the full [Getting Started][getting_started] documentation for more details, including code snippets and references.

## Running Locally

The application uses [Ruby](https://www.ruby-lang.org/) and [Bundler](http://bundler.io/) so you will have to download and install them as part of the setps below.

1. Copy the credentials from your `personality-insights-service` service in Bluemix to `app.rb`, you can see the credentials using:

    ```sh
    $ cf env <application-name>
    ```
    Example output:
    ```sh
    System-Provided:
    {
    "VCAP_SERVICES": {
      "personality_insights": [{
          "credentials": {
            "url": "<url>",
            "password": "<password>",
            "username": "<username>"
          },
        "label": "personality_insights",
        "name": "personality-insights-service",
        "plan": "IBM Watson Personality Insights Monthly Plan"
     }]
    }
    }
    ```

    You need to copy `username`, `password` and `url`.

1. Install [Ruby](https://www.ruby-lang.org/)
1. Install [Bundler](http://bundler.io/) with `gem install bundler`
1. Start the application with `ruby app.rb`
1. Go to `http://localhost:4567`

## i18n Support

  The application has i18n support and is available in English and 
  Spanish. The language is automatically selected from the browser's
  locale.
  
  To add a new translation follow the steps below:
  
  1. Translating the static text:
    1. Locate the `en.yml` file present in the `i18n` directory. This 
       file includes all the messages and labels in English.
    1. Copy `en.yml` and name the new file with the format `ll-CC.yml` or 
       `ll.yml`, where `ll` is the language code and `CC` is the country 
       code. For example, a new translation for argentinian Spanish would 
       be named after `es-AR.json`. You may omit the country code to make 
       the translation global for the language.
    1. Translate each English string to the desired language and save it.
  1. Translating the personality summary:
    1. Locate the JSON files present in `public/json/` directory.
       These are:
         * `facets.json`
         * `needs.json`
         * `summary.json`
         * `traits.json`
         * `values.json`
    1. Copy each file and name it with the format `<filename>_ll-CC.json`
       or `<filename>_ll-CC.json`. For example, a Portuguese language
           translations for `facets.json` will result in a new file named 
           `facets_pt.json`, an UK English translation for `traits.json` will
           result in a new file named `traits_en-UK.json`.
    1. Translate all the strings present in the new files to the desired
       language and save them.

## Troubleshooting

To troubleshoot your Bluemix app the main useful source of information are the logs, to see them, run:

  ```sh
  $ cf logs <application-name> --recent
  ```

## License

  This sample code is licensed under Apache 2.0. Full license text is available in [LICENSE](LICENSE).
  This sample code uses d3 and jQuery, both distributed under MIT license.
  
## Contributing

  See [CONTRIBUTING](CONTRIBUTING.md).

## Open Source @ IBM
  Find more open source projects on the [IBM Github Page](http://ibm.github.io/)

[personality_insights]: http://www.ibm.com/smarterplanet/us/en/ibmwatson/developercloud/doc/systemuapi/
[cloud_foundry]: https://github.com/cloudfoundry/cli
[getting_started]: https://www.ibm.com/watson/developercloud/doc/common/
[sign_up]: https://apps.admin.ibmcloud.com/manage/trial/bluemix.html?cm_mmc=WatsonDeveloperCloud-_-LandingSiteGetStarted-_-x-_-CreateAnAccountOnBluemixCLI
