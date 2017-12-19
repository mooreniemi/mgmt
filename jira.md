# jira

## jira primitives

[Jira has a glossary, but I'm going to try to give you
a TL;DR.](https://confluence.atlassian.com/agile/glossary)

### teams

j/k! jira actually doesn't have a team as a primitive without plugins!
(The most popular plugin seems to be Portfolio.) Instead, jira has groups.
Groups typically correspond to permissions groups.

__Tip: need to search for Issues by a Group in JQL?__

```
project = PROJECT_NAME AND reporter in membersOf("group-name")
```

### issue

An Issue represents a unit of work.
[Stories](https://confluence.atlassian.com/agile/glossary/story) should
represent delivery of customer value, Bugs should be self-evident to this
audience, and
[Tasks](https://confluence.atlassian.com/agile/glossary/task) are defined
as subunits of a Story, but I've found they have utility for us in
capturing ops work. This way we can see our ops burden versus our direct
delivery of customer value.

### epic

An Epic is just a type of Issue, but acts as a parent to many Issues.
While a Story should be completed within a single Sprint, an Epic may span
several Sprints. Epics should, however, be completable. If they are
open-ended, a Component is the better way to group Issues.

### [project](https://confluence.atlassian.com/jira064/what-is-a-project-720416135.html)

Simply: a collection of issues. Examples:

- a software development project
- a marketing campaign
- a helpdesk system
- a leave request management system
- a website enhancement request system

Projects define the KEY of an issue. So a Project called Baseball might
generate a key like BASE-1212124.

Projects can be given
[Categories](https://confluence.atlassian.com/adminjiracloud/adding-assigning-and-deleting-project-categories-844500732.html)
so "so your team can view work across related projects in one place" but
they "cannot be used to create project hierarchies (such as parent
projects)."

### [component](https://confluence.atlassian.com/adminjiraserver073/managing-components-861253335.html)

A Component is a logical grouping of issues in a Project. Examples:

- documentation
- backend
- email subsystem
- gui

For the example of a "website enhancement request system", Components
might include "Products", "Contact Us", etc... You'll notice while these
_could_ map to teams, I've never seen anyone use them to represent teams
except us!

There's also a such thing as
[sub-components](https://www.atlassian.com/blog/jira-software/organize-jira-issues-subcomponents)
if you need further granularity.

### versions

You can think of a Version as logical grouping of
issues by time, rather than any conceptual grouping of a Component.

If you switch to Kanban Versions become more important, because in order
to remove Issues from the board you need to release a Version. That's
usually done by actually literally doing a release of your software, but
doesn't have to be.

## what data can we get out of jira that helps us?

Jira is just a tool. If you put garbage in, you'll get garbage out. If you
automate status changes (using jira's API) and keep good team discipline
about changing statuses you can't automate, you can get a good picture of
how your team spends its time.

### jql

Dashboards and reports and sprint boards are all views created by JQL
queries. If you're familiar with SQL, JQL will look very approachable to
you. (There are even
[plugins](https://marketplace.atlassian.com/plugins/com.kintosot.jira.jdbc4jql/server/overview)
to directly translate between the two.) With some deeply annoying
exceptions, pretty much everything you put into jira can be easily queried
over and used to generate new views on your work.

__Tip: The biggest stumbling block I see when people are creating or
editing things on jira is that they don't make sure the permissions are
open to the right groups.__

### my favorite jira chart

[The Control
Chart!](https://confluence.atlassian.com/agile/jira-agile-user-s-guide/using-a-board/using-reports/viewing-the-control-chart)

I recommend looking at the control chart during every Sprint retro along
with your Sprint burndown chart. The control chart can help identify
bottlenecks in your process that slow down delivery. As an example I'm
going to pick on my team.

Looking at the control chart we identified that time spent in "Review" was
often several days. After identifying that bottleneck we made a commitment
to prioritize reviews. This meant checking in stand up on who is on
a review and making sure reviews were balanced across free team members.
We can't prove it's related, but you can see after mid-October and early
November our time spent in "Review" went down and also narrowed its
standard deviation.

Meanwhile if you look at our time spent in "Done" the standard deviation
is large and the trend is vaguely upwards. This suggests we should
prioritize things like continuous deployment so that stories can get to
launched faster.

One issue with the control chart is outliers. To deal with this, I've
manually tagged some issues that we don't think gave good data with the
label "outlier". This can happen because someone forgot to change the
status on time or some other random event we think isn't actionable to us.
