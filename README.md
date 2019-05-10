# Scroll-Columns
Imagine you have a grid with many many (many!!!) columns...
How do you scroll? By using scrollbar, normally... 
In this page you can scroll columns horizontally (forward and back) directly on the cell element you have the focus.
It does not matter how long is the cell, it scrolls automatically in the exact point of the next (or previous) element.

Basically we will consider two events on the generic cell of the grid:
* hover(), when the mouse points on the cell
* mouseleave(), when the mouse leave the cell

and also the click event on the two buttons of the cell, left and right arrows.

Let see what happens on these events:

```
//declare a js variable to store the scrolled position;
var scrolled=0;

//define the two html objects for left and right buttons;
var back= $("<i class='back fas fa-arrow-alt-circle-left' title='scroll left'></i>");
var forward= $("<i class='forward fas fa-arrow-alt-circle-right' title='scroll right'></i>");
 

$(".col-sm-1").hover(function()
{	
  //if in the selected cell the left and right do not exist, I will add them before and after the element
  if ($(this).children(".back").length==0 )
    $(this).prepend(back); //insert before the element
     
  if ($(this).children(".forward").length==0 )
    $(this).append(forward); //insert after the element
});

$(".col-sm-1").mouseleave(function()
{					
  // remove the arrows elements when the selected element is left
  $(this).children(".back").remove();
  $(this).children(".forward").remove();
});

// click event on the back arrow. Note that this element will be dynamically created, so that the click event will be attached starting from $(document).

$(document).on("click", ".back", function()
{
  //To go back to the previous element, the .prev() is used and than the the width of this element (outerWidth) is stored in len.
  var len=$(this).parent().prev().outerWidth(true); 
  scrolled=$(".container1").scrollLeft(); //the current position is get
  scrolled=scrolled-len;   // and the updated

  // here the new position is applied to perform the animation.
  $(".container1").animate({
      scrollLeft:  scrolled
  });
});

// the forward click is exactly the same of the back click with the only difference to use .next() instead of .prev() to get the element to consider.
$(document).on("click", ".forward", function()
{
  var len=$(this).parent().next().outerWidth(true);
  scrolled=$(".container1").scrollLeft();
  scrolled=scrolled+len;        

  $(".container1").animate({
   scrollLeft:  scrolled
  });
});

```

Demo: https://codepen.io/skepee/pen/xMqYRx






# Scroll-Columns - Highlight row and column
This version highlights the entire column and row of the selected element. Also navigation is showed.
 - When you scroll with focus on the header, the entire column is highlighted.
 - When you scroll with focus on a not header cell, the entire row is highlighted.

Demo: https://codepen.io/skepee/pen/VgOBGx
