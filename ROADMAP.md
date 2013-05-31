ROADMAP
============


Overview
---------

  Version 1.0 of this application is all about connecting people who can give help with people
  who need help.

  See www.help4ok.org as a proof-of-concept of the type of site and user
  experience this project aims to support.

  Below are checklists of user stories, functional requirements, and technical
  specifications we're aiming to fulfill for the 1.0 release.


Functional requirements for version 1.0
-----------------------------------------

  [ ] 1. Mobile: This website is 100% mobile first. (Perhaps better described as
      mobile-only. As cool as it would be to have a fancy responsive design and both
      a desktop and mobile version of the site, this is a nice to have. The must
      have is: Make this site super user friendly for users on mobile devices.)

  [ ] 2. Homepage: Simple "give help"/"need help" buttons as seen on help4ok.org.

  [ ] 3. First inside page (get here by clicking any of the main give/need
         buttons on the home page): This page should show me a list* that is
         filtered based on the button I clicked. If I need help, I should see a
         list of offers matching the type of help I need (e.g. if I need a ride,
         I should see a list of people offering to give a ride in their car). If
         I am trying to give help, I should see a list of people who need the
         type of help I can offer. (e.g. People who need rides.)

         If I don't see a match in the list, I should be prompted to create a
         new post (with an offer to help, or a request for help).
         
         If I find a match I should be able to claim it / unlist it.**

         * The list is a Drupal View (see technical specs below).
         ** Change the status of a give/need post using Flag (see tech specs).

  [ ] 4. If I don't see a match (see #3)...

           Prompt user to log in or register if they are anonymous.

           Then send user to node/add/post to post a new request/offer. (As seen
           on help4ok.org.)

  [ ] 5. As an authenticated user I should have some easy way to review:
         - My posts
         - Offers for help I accepted
         - People who accepted my offers to help

  [ ] 6. As a site admin, I should have a single form to fill out
         and save to add new types of help* that people can offer/request on the site. 
         Then new give/need buttons appear on the front page, with all the
         expected, cooresponding site functionality.**

         * Types of help should be Drupal taxonomy terms. The form
           should be a term with fields. (See tech specs below.)

         ** If the main listing page is one filtered View, filtered different
            ways depending on which link you click on the homepage. All posts
            requesting/offering help can be a single "post" content type. (See
            tech specs below.)

  [ ] 7. Site navigation: Drop down menu as see on help4ok.org.

  [ ] 8. Privacy settings: Site administrators should be offered different privacy
         options to choose from, as a list of radio buttons. When the administrator
         makes a selection and clicks save, corresponding rules and a corresponding
         privacy policy should be enabled. (We need at least two privacy settings:
         A. Show contact info on the site without requiring users to be logged in.
         B. Require users to log in before being able to access anyone's contact
         information. If we can add additional fancy options with VOIP Drupal
         integration, etc., great. But these two are the MVP.)


User stories for version 1.0
------------------------------

  [ ] As someone getting started with the Help distro, I should be able to
      download it from drupal.org/project/help, follow the install instructions, and
      get up and running with a fully functional site with very little fuss, and
      clear guidance step-by-step through site setup.

  [ ] As someone with help to give, I should be able to easily, quickly figure
      out who I can give help to, or offer my assistance to people who look me up
      thorugh the site.

  [ ] As someone in need of help, I should be able to easily, quickly find
      people who can help me, or post a request for assistance for people to find me
      through the site.

  [ ] As a person offering or requesting help, I should be able to easily,
      quickly update the site, so that once needs are met (e.g. someone fills a seat
      in a car, a bed in a home, etc.) there's not confusion or duplication of
      effort.

  [ ] As a site administrator I should be able to easily add new types of help
      for people to give and receive through the site.


Technical specifications
-------------------------

  [ ] 1. One main node type: Post

           Fields:
            - Title
            - Contact Info (collapsed fieldset)
              - First name
              - Last name
              - Phone
              - Email
              - Language
              - Preference (to be contacted by phone/voice, phone/text, email)
            - Location (collapsed fieldset)
              - [Address type info]
            - Notes (textarea / body field)
            - Help (text list, "request for help" or "offer to help",
              prepopulated by nodereference_url or path argument)
            - Help type (taxonomy term, e.g. "housing" or "ride", prepopulated
              by nodereference_url or path argument)
            - Help status (flag, note: this should probabably be themed to
              display as a check box or something visual, text-based flags are
              often confusing. Example: See DrupalLadder.org / drupalladder
              project checkboxes for marking lessons complete.)

  [ ] 2. Vocabulary: Types of help

          Fielded taxonomy terms (this should be the main site admin form with some form
          alters and theming to make this super user friendly)

          Fields might include things like:
            Short name (taxonomy term, default field)
            Need help text (to be used on "request" button on homepage)
            Give help text (to be used on "offer" button on homepage)
            Message to user who needs help (to be displayed on node/add/post)
            Message to user who can give help (to be displayed on node/add/post)
            Enabled (enable site admins to "disable" types of help to turn
              buttons on homepage off or on?)

  [ ] 3. Help buttons on homepage...

        Possible implementations should consider leveraging:
          https://drupal.org/project/taxonomy_menu
          https://drupal.org/project/menu_block

       Help block
         Unordered list with request help and offer help text and links.

         This block should be the main form of navigation presented in the content
         area on the home page.

  [ ] 4. Main menu

        Possible implementations should consider leveraging:
          https://drupal.org/project/taxonomy_menu
          https://drupal.org/project/menu_block

        Help menu
          Set to main menu.
          List of need/give help options.
          Mobile friendly dropdown like help4ok.org.

  [ ] 5. Install profile

          help.profile
          help.info
          help.install
          help-build.make (note: this include patch to core help module to rename it: help_core)
          drupal-org.make
