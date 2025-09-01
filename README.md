# Automation_rules
Rules for writing automation:
 
A- Avoid Delays:
 
1- Use .WaitForAsync() before .ClickAsync()
If not working, Use .WaitForAsync with Timeout: .WaitForAsync(new(){Timeout = 30000 })
 
2- If waiting for a page, Use WaitForResponseAsync();
example:
var url = "**/api/Fields/result";
var response = this.driver.Page.WaitForResponseAsync(url, new() { Timeout = 60000 });
await this.driver.Page.Locator("kqc-custom-time-field").First.ClickAsync();
await response;
 
3- If Waiting for skeleton to disappear:
await this.driver.Page.Locator(".flat-view-skeleton-container").WaitForAsync(new() { State = WaitForSelectorState.Hidden, Timeout = 15000 });
 
4- Instead of using delay then .InnerTextAsync(), use .GetByText("").WaitForAsync();
 
5- Instead of using delay then .IsVisibleAsync(), then assert it is true, use WaitForAsync() with timeout
 
6- Instead of using delay then .IsVisibleAsync(), then assert it is false, use .WaitForAsync(new(){ state = WaitForSelectorState.Hidden }) with timeout
 
7- Try not to use delays in loops even if only one second.
 
B- If you need to see the selector when it is not in the view: use .ScrollIntoViewIfNeededAsync()
 
C- When typing inside input: if not working correctly add small delay: use PressSequentiallyAsync("...", new(){ Delay = 200 })
 
D- When Using Assert.AreEqual() set the expected value first
 
E- Instead of using database queries in loops, use only one query that fetch all needed data at the beginning before the loop, then inside loop, apply linq on the fetched data.
