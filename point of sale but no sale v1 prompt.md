### point of sale no sale prompt

i have an application idea to help track catering orders for boast coffee

during catering events, we'd like an idea of how many drinks we sell so we can track inventory costs and also how much product we actually sell, since catering is a flat fee based on hours and what kind of menu offerings we have

right now we're just estimating it, because we don't use a POS system (there's no need to make a sale), it would just slow us down

because it's prepaid, we don't care about charging money or a payment solution, the idea is to track orders and see how much we're selling

there's a custom made opportunity here where we can start getting data by entering what drinks folks are getting, a simple solution is below, but feel free to suggest other things

we're mostly going to be working on mobile/ipad for this solution

 on the header, there's going to be a place where we can input the catering event that we're at. This should create a unique ID in the back end called catering name-hash(catering name + todays date)-# (0 to n) (as the orders come in)

catering-hash(catering name + todays date) will be in a table called events with start and stop times of the event

we start the timer when the event starts, and we start taking orders

on the main page, there's going to be a menu where we can select items: latte, vanilla latte, mocha latte, matcha latte, cappuccino, flat white, cortado, espresso

for each of those drinks there's gonna be an option for iced or hot, whole milk, almond milk, oat milk. Add a shot, add syrup decaf option

once we select our options, we hit done, and an abbreviated set of letters come up (what we write on the cup), since we're doing this already, we might as well have a machine generate it for us so we don't make mistakes, while having data taken down

VL, L, ML, MBL, O, A, WM, +shot, +vs, +s, -s something like that

for example the notation will be

VL
WM
+VS

denothing vanilla latte, with whole milk, add vanilla syrup

after we hit done, a row is inserted into a table called (orders)

with catering-hash(catering name + date)-1 (first order), timesteamp, order iced or hot / item / milk / modifications

there will be a live ordering view that we can delete rows if we make a mistake

and when we hit end timer, that end time is recorded in the events table

---

ok so i have some improvements to make

i don't really understand the "switch" button, that's pretty unintuitive, it just kills my current session

i can't see the text when writing in the event name up top at the beginning

i want a page where i can see past results (i think i created two dates), i want the ability to look the past live order and past summary and also have the ability to delete an entire date 

also, the black bar where we have the shorthand, let's have that right before the done at the bottom, so the barista's movements are all downward

for espresso, let's remove all of the milk options, there's no milk

for SHOTS, let's rename it extra shots

for SYRUP, let's rename to extra syrup, vanilla, mocha, maple bourbon as options
