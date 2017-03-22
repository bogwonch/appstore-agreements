% Summary Of App Store Terms And Conditions 
% Joseph Hallett
% 17 December 2014

User terms
==========

User Identification
-------------------

Yandex
:   For free apps no ID is required. For paid apps they must be an *authorized user*. They must provide payment details.

    'yandex' says User:U canBuy(App;A)
      if A isFree.

    'yandex' says User:U canBuy(App:A)
      if U isAuthorized,
         U hasPaymentDetails(P).


Google Play
:   Name, address and billing details (which may be shared with third parties.)

    'google' says User:U isAuthorized
        if U hasName(Name),
           U hasAddress(Address),
           U hasPaymentDetails(P).

    'google' says ThirdParty:P canKnow(User:U).

Amazon
:   Amazon account.

    'amazon' says User:U isAuthorized
      if U hasAmazonAccount(A).

Aptiode
:   ID and contact details. You agree not to provide false information. In practice when using the app no ID is required.

    'aptoide' says User:U isAuthorized
      if U hasID(ID),
         U hasContactDetails(D).

Apple
:   Apple ID 

What information do they take
-----------------------------

Apple
:   Technical data about the device, system, software and peripherals; which the Application Provider may use provided it is in a form that does not personally identify the user.    

Yandex
:   Type and model of the mobile device, OS, mobile app version and identifier, list of content on the device, usage info of apps and various services, mobile number and SIM serial number, geolocation info (which the user may deny), search queries, other *technical* information.


Google Play
:   App installation data (for malware checking.) To make this service more effective they also take device ID, URLs, one or more cookies[^1]. You may opt out of malware checking however.

Amazon
:   They *will not* access files or other information unrelated to the appstore. They will collect device info, network connectivity, download info (connection info I think, e.g. download speed), location, info about when an app is launched and usage info (including how long it ran for).

Aptoide
:   Transaction information, which they may share with developers.

How do you pay
--------------

Yandex
:   Through an approved processor provided by Yandex or the supplier.

Google Play
:   Google Wallet, and others at Google's discretion.

Amazon
:   Through Amazon.

Aptoide
:   Through an approved partner's payment processor.

Apple
:   Through a credit/debit card or gift card.

Who pays whom
-------------

Yandex
:   The user pays the supplier of the app (the developer)

    'yandex' says User:U mustPayFor(Supplier, Purchase:P)
      if U hasPurchased(P),
         Purchase isSuppliedBy(Supplier).

Google Play
:   The user pays Google Commerce or the a provider where Google is acting as an agent.

    'google' says User:U mustPayFor('google-commerce', Purchase:P)
      if U hasPurchased(P).

Amazon
:   User pays Amazon.

    'amazon' says User:U mustPayFor('amazon', Purchase:P)
      if U hasPurchased(P).

Aptoide
:   The store owner (through Aptoide)

    'aptoide' says User:U mustPayFor('aptoide', Purchase:P)
      if U hasPurchased(P).

Apple
:   The user pays Apple.  If a user use *family sharing* then the Family Organiser pays Apple.

    'apple' says User:FO mustPayFor('apple', Purchase:P)
      if U hasPurchased(P),
         U isInFamily(F),
         FO isFamilyOrganiserFor(F).

    'apple' says User:U mustPayFor('apple', Purchase:P)
      if U hasPurchased(P).

Who sets the prices
-------------------

Yandex
:   The supplier. Yandex *"has no control over the cost of the Content under any circumstances"* (Section 5.1.5.) In the developer agreement, however, Yandex say they *"may limit Your choice of the exact amount of End User Fees You wist to charge"*. (Section 4.2.) Yandex sets the currencies you specify your prices in but may convert the prices to other currencies. The supplier can change the prices at any time.

Google Play
:   The developer, however Google may round the price up to avoid fractional pennies and silly amounts. If the developer makes the app free they may not start make the app paid for later on.

Amazon
:   Amazon, but based on a minimum price or suggested price or actual price set by the developer.

Aptoide
:   The developer and the store owners[^2]. Aptoide may round prices.

Apple
:   Developer picks a price tier from Apple's list of prices.  Pricing tier used to set worldwide pricing.

Refunds
-------

Yandex
:   Available for fifteen minutes after paying for the content. For IAP there are no refunds.

    'yandex' says Purchase:P canBeRefunded
      if P isContent
      where age(P) < 0.25.

Google Play
:   Supposedly only for defective content, or content which has been removed from the store (and your device) by Google. However you may request a refund through the Play Store app for two hours after you purchase it. The developer agreement says that a refund for an amount less than 10 USD may be issued upto 48 hours after the purchase; for amounts above 10USD it depends on who processed the payment.

    'google' says Purchase:P canBeRefunded
      where age(P) < 2.

    'google' says Purchase:P canBeRefunded
      where age(P) < 48, amount(P) < 10.

    'google' says A can-say Purchase:P canBeRefunded
      if A hasProcessed(P)
      where amount(P) >= 10.

Amazon
:   No.

Aptoide
:   24 hours.

    'aptoide' says Purchase:P canBeRefunded
      where age(P) < 24.

Apple
:   14 days.

    'apple' says Purchase:P canBeRefunded
      where age(P) < 336.


Age of Use
----------

Yandex
:   Users must be at least 14. If beneath 18 they must have consent from their guardian.

    'yandex' says User:U canUseStore
      where age(U) >= 18.

    'yandex' says User:Guardian can-say
      User:U canUseStore
      if Guardian isGuardianOf(U)
      where age(U) >= 14.

Google Play
:   Users must be at least 13. If beneath 18 they must have consent from their guardian.

    'google' says User:U canUseStore
      where age(U) >= 18.

    'google' says User:Guardian can-say
      User:U canUseStore
      if Guardian isGuardianOf(U)
      where age(U) >= 13.

Amazon
:   Bellow 18 with consent of a guardian. Nothing to do with alcohol under 21.

    'amazon' says User:U canUseStore
      where age(U) >= 18.

    'amazon' says User:Guardian can-say
      User:U canUseStore
      if Guardian isGuardianOf(U)
      where age(U) < 18.

    'amazon' says User:U canSeeRestrictedContent
      where age(U) >= 21.

Aptoide
:   You must be of a legal age to form a contract with Aptoide, and not be barred from using Aptoide in the laws of your country[^3].

    'aptoide' says User:U canUseStore
      if U isFromCountry(C),
         Age isLegalAgeIn(C)
      where age(U) >= Age.

Apple
:   Must be 13 or older (or equivalent minimum age in home country) to create an apple ID.  Parents or legal guardians can create an ID for you through Family sharing, or by an approved educational institution.

    'amazon' says User:U canUseStore
      where age(U) >= 13.

    'apple' says User:Guardian can-say
      User:U canUseStore
      if Guardian isGuardianOf(U).

    'apple' says 'educational-institution' can-say
      User:U canUseStore.

Updates
-------

Yandex
:   The user has to understand that Yandex may update the content on their devices for security and bugfixing reasons.

Google Play
:   Google will check for updates and you agree to receive them[^4].

Amazon
:   By default they'll install updates, but this can be changed.

Aptoide
:   You agree that Aptoide can check for apps and you will receive updates.

Apple
:   No obligation (but the default is to install them).  Developers are resposible for maintaining their software.

Store Moderation
----------------

Yandex
:   They may moderate and filter content, but are not obliged to.

Google Play
:   No obligation to but Google may.

Amazon
:   Publisher is obliged to provide (accurate) info about the app, which may be used to give ratings. Amazon cannot check these ratings are accurate.

Aptoide
:   Aptoide may review, screen, modify and remove apps but is not obliged to. The Aptiode *trusted app* sign indicates an automatic virus checker has checked the app and *does not* imply Aptoide actually checked it.

Apple
:   Nothing I can see, however they do have a stringent review process.

What can you do with the content
--------------------------------

Google Play
:   You cannot use apps as part of a *public performance*. You may transfer apps between linked Google accounts. You may not use content for *dangerous activities*, such as nuclear plants, life support, emergency communications of aircraft control or other similar activities where failure might lead to death, injury or environmental damage.

Aptoide
:   You may not modify, rent, lease, loan, sell, distribute or create derivative works based on this Content. You may use the software.

Apple
:   Apps are licensed to you not sold.  You may use the content on only Apple devices.  If the device is later sold you must remove the content before selling.  You may not distribute, copy, reverse-engineer, disassemble, attempt to derive the source code of, modify, or create derivative works of the Licensed Application, any updates, or any part thereof.


Others
------

Yandex
:   Yandex offer a *bonus scheme*, where they give users 10% credit for all purchases. These bonuses must be used with 36 months of the receipt of the bonus (when they pay). If the user terminates their account they lose all bonuses.

Google Play
:   Pre-orders are processed as soon as the product is available as a normal product. You can cancel a pre-order at any time. Copy and paste cannot be for commercial purposes.

Developer Terms
===============

What can they do with your app
------------------------------

Yandex
:   Yandex can use your marks, names, logos and images of your content worldwide, for marketing your apps and advertising their store. Yandex may sublicense this right to a third party.

Google Play
:   Google can reproduce, perform, and display the app for marketing, demonstration, improving Android and *administrative* purposes Google may delegate this to a third party.

Amazon
:   Irrevocable, royalty free right to: distribute through all electronic means (now and future) your app, evaluate and test your content, reproduce and store your app. Amazon may modify and add to your app for analytics, policy enforcement, and metadata to improve compatability with Amazon devices. Amazon may at the developers request add DRM. Amazon may use your app to promote and advertise. Amazon may make diferent versions of your app for limited time promotions or creating *test drive* versions. Amazon will keep a copy of your app, and may claim other addition rights.

Aptoide
:   Sell and make available to third party stores. Possibly modify (it is hinted in the user agreement that Aptoide may).

How quickly will they remove an app from a store
------------------------------------------------

Yandex
:   Within 90 days on request from the developer. Yandex keep an archive copy.

Google Play
:   You may request an app to be removed. If it's for infringement of IP or law then users who downloaded within a year are entitled to a refund.

Amazon
:   10 days normally, and 5 days if it is due to a loss (or third party claim to) rights described in their terms. ASAP if it is due to breaking terms or the law.

Aptoide
:   You may remove your products from the marketplace and third party markets but they don't give a time period.

Developer ID
------------

Yandex
:   Email, company name, tax-id, addresses, country of residence, website, order email, user support email (and an urgent one for Yandex only[^5]), payment information as well as *other reasonable information*.

Google Play
:   Google account and payment info.

Amazon
:   Amazon account

Aptoide
:   Email. Using the same email you use as a Google Play developer account may speed apps through the store.

Apple
:   Apple Developer ID.

EULA
----

Yandex
:   Developer must provide one and it must include the right to the content worldwide (except for trials.)

Google Play
:   Developer may provide one otherwise the user is granted the worldwide perpetual right to perform, display and use the product.

Amazon
:   You can provide one if it doesn't interfere with any Amazon terms.

Aptoide
:   They provide a default one, but suggest developers may provide one that supercedes it.

Apple
:   You must provide one or accept the default.

Content Restrictions
--------------------

Yandex
:   Content must be safe, free of defects, and described accurately. Nothing disruptive to Yandex or malware. Nothing illegal such as: child pornography, obscenity, nudity, sex, extremist, hatred, violent, discriminatory, defamatory gambling, copyright infringement, or other forbidden material. Nothing that steals private information. Nothing mimics system functionality. Nothing that would require Yandex to open source anything via copy-left. No alternative marketplaces.

Google Play
:   No alternate stores. No sex, violence, bullying, hate, impersonation, IP infringing, PII publishing (credit cards, ID card numbers, or non-public contacts), illegal content, gambling, dangerous (malware or spyware), self-modifying, or system interfering content.\
    No unpredictable network use.

Amazon
:   No offensive content, pornography, illegality, gambling with real currency, IP infringing, privacy infringing, copyright infringing. Nothing that would be illegal in the country that the app would be sold.

Aptoide
:   Nothing that displays or links to: illegal content, invasions of privacy, content that interferes with with the services of others, hate or violence, IP infringing material. Nothing that harms devices or personal data. Nothing that has unpredicable nework usage or has an adverse impact on a user's service charges or a carrier'n network. Nothing that creates a *"spammy user experience"*.

Who describes your content
--------------------------

Yandex
:   Developer, though Yandex can change it at their discretion.

Google Play
:   Developer.

Amazon
:   Developer, but Amazon can edit it.

Aptoide
:   Developer.

Who can distribute your content
-------------------------------

Yandex
:   Yandex and partner stores.

Google Play
:   Google.

Amazon
:   Amazon and regional subsidiaries.

Aptoide
:   Aptoide and third-party partners using Aptoide to create their own store.

What support must the developer provide
---------------------------------------

Yandex
:   Must provide users with support via email or phone. Must respond to users within 5 days.

Google Play
:   Developer must support their app and handle complaints. Developer must respond within 3 days, and to issues Google deem urgent within 24 hours. Failure to do so will result in Google lowering your apps ranking and review scores or removal.

Amazon
:   5 days generally, 24 hours for any issue identified as critical by Amazon.

Aptoide
:   Aptoide will give your contact information and you are solely responsible for support, however it doesn't say any support must be provided.

What privacy guarantees must you provide
----------------------------------------

Yandex
:   Must make the user aware as to what info you gather and for what purposes. Must not go past theses purposes without notification (unless its in your EULA that you can.) Ensure that you keep the data safely.

Google Play
:   That you will behave as you describe in your EULA. If you take any usage info, or login (username, password) or personal information you will provide a privacy policy. You will not hold personal information for longer than required, and you will hold it securely.

Amazon
:   If you collect name, password, other login information, or personally identifiable information or personal data of any end user based on any use of or interaction with your Content, then you must provide a privacy policy. You must ensure all information is collected, trasfered and stored in the way you describe, and in accordance with local laws.

Aptoide
:   Developer will protect the privacy and legal rights of users. If you collect product uses, usernames, passwords, or other PII or login inf you will privide a privacy policy. If you process this data you must do so securely and only store it for the minimum amount of time. If a user provides you with information to get into their Aptoide account you will only use this for the purposes you agreed with the user to.

When do you get paid
--------------------

Yandex
:   30 days after the end-of-the month of the purchase; provided you have accrued more than 100 USD. If you earn less than that Yandex will accrue it without interest.

Google Play
:   On the 15th of the following wonth via Google Wallet. Minimum earned balance for local currency payout is 1USD. 100USD for wire transfer payouts.

Amazon
:   Roughly 30 days after the app was sold

Aptoide
:   Roughly 30 days after the end-of-the mont of the purchase.

What do you get paid
--------------------

Yandex
:   70% of the net revenue (minus transaction fees.)

Google Play
:   70% of the payment paid by the user.

Amazon
:   70% of the list price (minus card processing fees.)

Aptoide
:   75% of revenue share after deduction of all transaction fees. Other rates subject to agreement with Aptoide.

Other
-----

Google Play
:   25 USD fee to distribute apps.

Amazon
:   Families can use a *family library* feature to share apps for free between family members.

[^1]: This implies they have a specific cookie in mind?

[^2]: Aptoide allows individuals to curate their own stores which may possibly set more other prices? It isn't clear.

[^3]: This seems to be a bit of a catchall. I'm assuming it means laws against computer criminals using computers, perhaps certain groups in repressive regimes?

[^4]: But does this mean install them?

[^5]: Does this imply Yandex may sell the rest of your info?
