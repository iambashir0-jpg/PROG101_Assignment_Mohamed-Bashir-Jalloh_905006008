# SaloneMove: Algorithm

PROG101 Principles of Programming Logic and Design. Revised after examiner review.

The algorithm below describes, in plain English, what SaloneMove does from the moment a user dials the short code. Each part matches a module in the pseudocode (Section 3) and a flowchart (Section 4).

## Main Program

1. Start. Set attempts to 0 and isValid to FALSE, and display "Welcome to SaloneMove".
2. **Validation.** While attempts is less than 3 and isValid is FALSE: read the phone number. If it has 9 digits and starts with a valid mobile prefix (for example 076 or 088), set isValid to TRUE; otherwise add 1 to attempts and display how many attempts are left.
3. If isValid is still FALSE, display "Too many invalid attempts. Session ended." and stop.
4. **Verification.** Otherwise create a random six-digit code and send it to the number by SMS. If the SMS cannot be sent, display "Code could not be sent. Please try again later." If it is sent, allow up to 3 tries: a try succeeds only if the code typed matches and no more than 5 minutes have passed since it was sent; each failed try displays "Wrong or expired code." with the attempts left. If the number is not verified, display "Phone number not verified. Session ended." and stop.
5. Otherwise set running to TRUE. While running is TRUE, display the menu (1 Check a Fare / Report a Problem, 2 Officer Login, 0 Exit) and read the choice with ReadChoice, which accepts only 0, 1 or 2.
6. If the choice is 1, perform Check a Fare. If 2, open the Officer Portal. If 0, set running to FALSE.
7. When the loop ends, display "Thank you for using SaloneMove. Waka fine!" and stop.

## Check a Fare

1. Read the starting point and the destination with ReadPlace.
2. Show the vehicle menu (1 Poda-poda, 2 Keke, 3 Okada) and read the choice with ReadChoice (1 to 3).
3. Search the fare table from the first record. A record matches when its vehicle type is the one chosen and its route is the two places in either order, compared in capital letters. Stop at the first match; if there is none, the result is −1.
4. If the result is −1, display "Route not found. Check the spelling or try another vehicle." If the record's official fare is 0 or less (a damaged record), display "Fare record error. Please try again later.", so the percentage is never divided by zero. In both cases return to the menu.
5. Otherwise take the official fare and the route name from the matching record and set the status to NOT CHECKED. Show the fare and read the amount paid with ReadNumber, which accepts only a number from 0 (skip) to 10 times the official fare.
6. If an amount was entered, calculate difference = amount paid − official fare, rounded to 2 decimal places, and percent = difference ÷ official fare × 100. If the difference is more than NLe 0.50 below the fare, the payment is **UNDERPAID**; else if it is within NLe 0.50 either way, it is **CORRECT**; else if percent is 50 or more, it is a **SERIOUS OVERCHARGE**; otherwise it is **OVERCHARGED**. Display "Correct fare.", the amount underpaid with a request to pay the official fare, or the overcharge status with the amount and percentage.
7. Ask whether the user wants to report a problem with this vehicle and read the answer with ReadChoice (1 or 2). If the answer is 1 (Yes), perform Report a Problem with the route, the amount paid and the fare status.

## Report a Problem

1. Show the five problem types and read the choice with ReadChoice (1 to 5).
2. If the choice is Overcharging but the fare status is not OVERCHARGED or SERIOUS OVERCHARGE, display "Report refused: the fare check did not find an overcharge." and return.
3. Otherwise read the plate number. While it is not 0 and not valid (5 to 8 letters and digits once spaces are removed), display "Invalid plate number" and read it again. 0 means the plate was not seen.
4. Add 1 to reportCounter and build the reference number in the form SLM-YEAR-NNNNNN.
5. Save the complaint with the reference, phone number, plate (in capitals, without spaces), route, problem type, amount, fare status, date and time, and status OPEN.
6. Send an SMS with the reference number; if it cannot be sent, display "SMS not sent. Please write down your reference." Display the reference on screen.

## Officer Portal

1. If the caller's number is on the locked list, display "Officer login is locked for this number." and return.
2. Otherwise allow up to 3 PIN attempts. A PIN is accepted only if its hash matches the stored hash; each wrong PIN displays the attempts left. After 3 wrong PINs, add the number to the locked list and display "Access denied. Officer login locked for this number."
3. If the PIN is accepted, until the officer chooses 0, display the officer menu (1 Hotspot Report, 2 Apply Fare Change, 0 Back), read the choice with ReadChoice and carry it out.
4. **Hotspot Report:** for each route, count the complaints on that route that are still OPEN. If the count is 3 or more, display the route as a hotspot and add 1 to hotspotCount. At the end, display the total, or "No hotspots this period." if there are none.
5. **Apply Fare Change:** read the percentage with ReadNumber, which accepts only a number from −50 to 50. If it is 0, display "Rejected: the change cannot be 0%." Otherwise ask for confirmation (ReadChoice, 1 or 2). If confirmed, multiply every fare by (1 + percent ÷ 100), round to 2 decimal places and display how many fares were updated; if not, display "No changes made."

## Input Functions

Every number, menu choice and place name is read as text and checked before it is converted or used. If it is wrong, a message says what is expected and the user types it again. The phone number, verification code and officer PIN are different: they allow only 3 attempts, because repeated guessing there is a security risk.

1. **ReadChoice(low, high):** accepts only digits whose value is from low to high, and returns the number.
2. **ReadNumber(low, high):** accepts only a number from low to high, and returns it rounded to 2 decimal places.
3. **ReadPlace(prompt):** shows the prompt and accepts only letters and spaces, with at least 2 letters, and returns the place without spaces at either end.
