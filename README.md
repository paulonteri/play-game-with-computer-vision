# Python bot used to play the game 'City Island'

A python bot (powered by computer vision) used to play City Island 5.

Access a more comprehensive guide in this article here: [https://paulonteri.com/thoughts/play-game-with-computer-vision](https://paulonteri.com/thoughts/play-game-with-computer-vision).

Here's a screen recording of the game play:

https://user-images.githubusercontent.com/45426293/204757801-eb57b481-af30-45ed-ac0b-1741168783b6.mp4

---

## Why?

I've been playing strategy + city building + simulation? games like [TownsMen 6](https://play.google.com/store/apps/details?id=com.hg.townsmen6&hl=en&gl=US), [Clash of the Clans](https://apps.apple.com/us/app/clash-of-clans/id529479190), [SimCity](https://store.steampowered.com/app/24780/SimCity_4_Deluxe_Edition/) for the last 10 years.

On trying out [City Island 5](https://apps.apple.com/us/app/city-island-5-tycoon-sim-game/id1445023279?mt=12) I found it mildly irritating that my collectibles could not accumulate while I was outside the game. I might have had the best businesses, strategy, etc but I had to be in the game to ensure I collect the cash/keys/gold overtime. For example if my bakery makes €100 per minute I would only earn €100 after leaving the game and coming back 24 hours later.

This became especially tiresome while trying to accumulate €5,000,000 required to buy the island shown below. This would take me roughly two weeks of gameplay if I don't spend any money - it's not worth it.

<img width="995" alt="game_screenshot_island" src="https://user-images.githubusercontent.com/45426293/204755494-0fabfa0d-77df-4fa2-9474-9e6ebc8c4ebd.png">

---

## How it works

### 1. Capture the live game feed

I needed a way to capture the live game feed.

The easiest way to to capture an in-game screenshot and pass it to the next steps in the script.

### 2. Identify the valuables in the screenshot

We need a way to detect a valuable in the game's feed then return its coordinates.

`OpenCv`'s **Template Matching** algorithms are perfect for this.

They are used for searching and finding the location of a template image (like a valuable) in a larger image (like the game's feed). It simply slides the template image over the input image (as in 2D convolution) and compares the template and patch of input image under the template image. Several comparison methods are implemented in OpenCV. (You can check [docs](https://docs.opencv.org/4.x/d4/dc6/tutorial_py_template_matching.html) for more details). We use it in the method: `cv2.matchTemplate(... )`

To achieve this, I needed the template images. I took screenshots by hand then cropped off the cash, star and key:

<img width="32" alt="cash" src="https://user-images.githubusercontent.com/45426293/204754890-ee25befa-094d-4dfd-829c-1302165d64e0.png">

<img width="32" alt="key" src="https://user-images.githubusercontent.com/45426293/204755018-b2773061-5f18-4693-b586-792611f83eb1.png">

<img width="32" alt="star" src="https://user-images.githubusercontent.com/45426293/204755064-b68fd852-a0e5-4f11-a29e-276fe955bca1.png">


### 3. Collect the valuables by clicking on them

Once we have the coordinates of an item we can try to click on it.

`pyautogui`'s `.click(x,y)` function works like magic for this. It clicks the screen on the coordinates x and y where our valuable is lying.
Learn more about it [here](https://pyautogui.readthedocs.io/en/latest/mouse.html#mouse-clicks).

https://user-images.githubusercontent.com/45426293/204756803-38e48b98-1945-4ff7-b437-b73e58a97437.mp4

https://user-images.githubusercontent.com/45426293/204758224-7ee70df4-e937-41b7-997e-18092e2fea1e.mp4

https://user-images.githubusercontent.com/45426293/204758262-b07ade42-7114-4b94-bc37-874536786e0b.mp4

### 4. Close any popups that may appear

Our clicks above may result in popups when we are being given a reward, levelling up, etc.

We need to close it before attempting to collect valuables again. We use the same logic used in finding and clicking on valuables.

To achieve this, I needed the template images for the popups' close buttons so that they can be clicked. I took screenshots by hand then cropped off the various close buttons:

<img width="32" alt="close" src="https://user-images.githubusercontent.com/45426293/204755164-9321de98-465a-455e-8d85-e656b1c7f16b.png">
<img width="189" alt="continue_level" src="https://user-images.githubusercontent.com/45426293/204755189-b70fef92-4eea-444c-83be-00a7fbf49c36.png">

https://user-images.githubusercontent.com/45426293/204756326-4b3db64a-e5e1-4191-83c1-73b9c74b8f7d.mp4

### 5. Repeat

We do the steps above repeatedly to collect the valuables while the script is running.

https://user-images.githubusercontent.com/45426293/204757801-eb57b481-af30-45ed-ac0b-1741168783b6.mp4

---

## Results after running overnight

I started the game with €316,415.

<img width="1680" alt="game_screenshot_start" src="https://user-images.githubusercontent.com/45426293/204754488-83cfa0ec-b97b-4516-8a81-f7b852dd6008.png">

The following morning I had €6,463,870.

<img width="1680" alt="game_screenshot_start" src="https://user-images.githubusercontent.com/45426293/204754670-f8fd23ef-1b49-4e30-8414-87c32f2d6b31.png">

I made €6,147,455 overnight!

I then proceeded to buy the Island I wanted:

![image](https://user-images.githubusercontent.com/45426293/204755770-3499c14e-811e-465b-9196-e8a0604c863c.png)

---

## Regrets

- This is cheating.
- Why get a game if you're not the one playing it?

---

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

---

## Maintainers

Current maintainers:

- Paul Onteri - <https://paulonteri.com>

---

## License

[Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0)

---

## Conclusion

Access the full guide in this article here: [https://paulonteri.com/thoughts/play-game-with-computer-vision](https://paulonteri.com/thoughts/play-game-with-computer-vision)

This was fun!

