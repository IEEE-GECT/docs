# Adding a New Event in IEEE Website
## Things to be changed
1. Create a Page for typeform to get embedded
2. Links in Navbar, both in Mobile View and Web View
3. Upcomming  Events in Homepage


## Getting started by Cloning the Project and Installing

    git clone https://github.com/ieee-gectcr/web-core
    cd web-core
    npm install
    git checkout -b <new branch name>
    code .

## Creating a New Page

1.  Create a copy of an existing page in the same folder. (eg. if you need to create a new event registration page. Navigate to /pages/src/e/ folder and create a copy of an existing event page)
2.  The default route of an event page is set as "/e/{event-name}"
3.  Change the 'route' prop inside Layout Component an event page to match the url required by the event.

        <Layout route="/e/event-name">

4.  Pass the page title, description and meta-image as props into the SEO component

        <Seo
        title="title of page"
        description="decription of page as seen in whatsapp link share"
        image="https://url-link-to-image-as-seen-in-whatsapp-link-share"
        />
        
5.  Change the typeform embed code. Each typeform has a unique code. (eg. https://ieee-gec.typeform.com/to/dA8Hnzqs in this typeform link "dA8Hnzqs" is the unique typeform code). Insert this code to createWidget function in the event page.

        React.useEffect(() => {
         createWidget("typeform-code", { container: container.current })
         }, [])

6. Rename the eventpage to event-name.jsx where event-name is as given in the route

## Updating the Navlinks to Include the newly created event page in Registrations

Here we have to change two files. First file "header.jsx" changes the navlinks in Desktop view and second file "sidebar.jsx" changes navlinks in mobile view.

1.  In header.jsx

    Change the 'to' prop and child content to match the desired values. 'to' prop must have the route and child would be how the link would be named.
        
            <DropDownLink to="/e/event-name">Event Name</DropDownLink>

2. In sidebar.jsx

    repeat the same step and replace the 'to' prop and child inside the 'nav' tag.

        <nav>
          <NavLink to="/">Home</NavLink>
          <NavLink to="/chapters">Chapters</NavLink>
          <DropDown to="/e/" title="Registrations">
            <DropDownLink to="/e/event-name">Event Name</DropDownLink>
            <DropDownLink to="/e/event-name">Event Name</DropDownLink>
            <DropDownLink to="/e/event-name">Event Name</DropDownLink>
          </DropDown>
          <NavLink to="/execom">Execom</NavLink>
        </nav>

## Updating the Upcoming Events in Homepage
Here the file to be edited is 'slider.component.jsx' which reside in '/src/components/slider.component.jsx'
Find the SwiperSlide component and replace 'imgSrc' prop with image link and 'to' prop to event-page.

        <SwiperSlide style={{ maxWidth: 640, maxHeight: 640 }}>
          <SlideBody
            to="/e/event-name"
            imgSrc="link-to-image-on-slider"
          />
        </SwiperSlide>

Yup! you are ready to publish

## Publishing
1. git add and commit all changes

        git add .
        git commit -m "added event event-name"

2. git push to origin, remember the new branch name we created on start

        git push origin <new branch name>

3. deploy to gh pages for testing

        npm run deploy-gh

4. create a pull request to release branch and when merged the page update will be automatically deployed to the gec ftp server