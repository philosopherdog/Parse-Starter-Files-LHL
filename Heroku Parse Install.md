# Instructions For Installing Parse.org To Heroku

## Setting Your App Up On Heroku

* Create a Heroku account. You will need a credit card even though this is a free tier account.

* Once you have created an account and can log in then go to this link: [here](https://devcenter.heroku.com/articles/deploying-a-parse-server-to-heroku)

* Scroll down  until you see a purple button that says "Deploy To Heroku". CLICK button!

* Leave everything alone except the **appname**, **appid** and **masterkey**. Fill these in and copy paste somewhere convenient.

* Add your appname to the url

* e.g. http://crudit.herokuapp.com/parse

    * Here my app's name is `crudit` so this gets added to the url before .herokuapp.com

* Click deploy! Wait until the app shows that it was successfully deployed.

* You can view the app and click on mlab to view the db. We will return to this in a second.

### Installing Parse SDK & Testing

* You can install the Parse SDK using either Cocoapods, Carthage, or manually. If using Cocoapods make sure you update the pod spec file using: `pod install --repo-update`

* I omit the instructions for installation since I'm assuming you know how to do this. (See my Carthage instructions).

* Swift projects no longer require a bridging header.

* You should be able to import Parse into a Swift file once installation is complete.

* Let's save a test object to make sure everything's wired up correctly. (Old quickstart instructions can be found [here](https://docs.back4app.com/docs/ios/quickstart/))

* Add this to your AppDelegate:

```swift
private func configureParse() {
    let configuration = ParseClientConfiguration {
      $0.applicationId = "xxxx"
      $0.clientKey = "xxxxx"
      $0.server = "https://yourappname.herokuapp.com/parse"
    }
    Parse.initialize(with: configuration)
    let testObject = PFObject(className: "TestObject")
    testObject["foo"] = "bar"
    testObject.saveInBackground { (success: Bool, error: Error?) in
      guard error == nil else {
        print(#line, error?.localizedDescription ?? "No explicit error")
        return
      }
      guard success == true else {
        print(#line, "object not saved, WTF!")
        return
      }
      print("Object has been saved!")
    }
  }
```

* Run the app.

* Check the mongo db by clicking on mLab MongoDB :: Mongodb link in the heroku dashboard

### Installing Parse Dashboard Locally

* The instructions for Parse dashboard installation are [here](https://github.com/ParsePlatform/parse-dashboard).

* First make sure you have Node.js version >= 4.3 installed. Go to terminal and type `Node -v` to get the version if any. If it doesn't meet the requirement then install the latest version by going [here](https://nodejs.org/en/). Download and install it.

* With node installed, run `npm install -g parse-dashboard` .

* To view your app you have to enter the following into terminal, and fill out the places for `yourAppId`, `yourMasterKey`, `https://example.com/parse`  with your url and `optionalName` in the following script `parse-dashboard --appId yourAppId --masterKey yourMasterKey --serverURL "https://example.com/parse" --appName optionalName`. Paste the command into an editor and change those values then copy/paste into terminal and run.

* Now open your browser to `http://localhost:4040`

