# Problem

Setting the contentOffset of a UIScrollView does not work inside a `viewDidLoad` or `viewDidAppear` method of a *UIViewController*.

# Solution
*Extracted from http://stackoverflow.com/questions/25916000, answer by Nick*

Set the contentOffset of a UIScrollView inside the `viewDidLayoutSubviews` method of the corresponding *UIViewController*.

````
-(void) viewDidLayoutSubviews
{
  [self.someScrollView setContentOffset:CGPointMake(0, 100)]; // Set contentOffset to point (0, 100)
}
````

