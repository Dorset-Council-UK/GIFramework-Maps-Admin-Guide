# Tours

Tours are used to give users a quick overview of the features of GIFramework Maps. Tours are highly configurable, and different tours can be applied to specific versions.

## Add a new tour

Select **Create new tour** and fill in the details:

- Name of your tour
- How often you want the tour to display
- Update date - a date when the tour has been updated enough to reshow it to users

Once you've created a tour, you can start adding individual steps. To do this, either tick the *Add step on save* box when you're creating your tour - or create your tour, click on it again and you'll see an option to create tour steps on the right.

When you're creating a tour step, you'll need to fill in the following:

- Title - this text will appear in bold at the top of the tour step
- Content - what you want your step to say. You should include HTML markup for links and also `target="_blank"` as this will make sure the link opens in a new window 

!!! example
    `<a href="https://gi-staging.dorsetcouncil.gov.uk/dorsetexplorerdocs" target="_blank">Help pages</a>.`

- Name of the selector you want the tour step to attach to (include the '.'), if you leave this blank the tour step will float in the middle of the screen

!!! example
    `.sidebar-button-share`
    or
    `.search-control`

- Where on the selector you want the tour step to attach (if you've chosen one)
- Step order - this number will start at 1 and increase as you add more steps. If you want to alter the order that the steps appear, change this number

## Edit a tour

Select the tour or step you want to edit. Make the changes you want and hit Save.

## Delete a tour

Select the tour or step you want to delete. You will be asked if you're sure, press Delete again to confirm.