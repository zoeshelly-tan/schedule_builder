# schedule_builder

>purpose: this website is build for users to arrange their schedule inside.


- Read the current date to remind the user with the date. 
   ```js
    const time = moment().format("MMM DD YYYY");
      console.log(time.toString());
      $("#currentDay").text(time.toString());
      ```
- Create a loop to build the time labels, inputs and the buttons.
  ```js
      function Scheduler() {
        var h = 9;
        for (var i = 0; i < 9; i++) {
          var format = $("<div class='input-group mb-3'>");
          var hour = $("<span class='input-group-text'>");
          var input = $("<input>");
          var save = $("<button>");

          input.attr({
            class: "form-control",
            placeholder: "your day",
            id: "planinput" + i
          });
          if (h <= 12) {
            hour.text(h + "AM");
          }
          else if (h >= 12) {
            h = 1;
            hour.text(h + "PM");
          }
          hour.attr("id", i);
          h++;
          save.attr({
            class: "btn btn-outline-secondary"
          });
          save.text("Save");
          format.append(hour, input, save);
          $(".container").append(format);
        }
      }
      ```
- Save the input text to the local storage.
    ```js
      function saveSheduler() {
        $("button").on('click', function () {
          var inputDayplan = $(this).prev().val();
          var time = $(this).prev().prev().text();
          console.log(inputDayplan)
          localStorage.setItem(time, inputDayplan)

        })
      }
      ```
- To display the local storage to the right input box. 
    ```js
      function displayData() {
        for (var i = 0; i < 9; i++) {
          var spanId = "#" + i;
          var key = $(spanId).text();
          console.log("timeKey " + key);
          var storedVal = localStorage.getItem(key);
          console.log(storedVal);
          var inputId = "#planinput" + i;
          $(inputId).val(storedVal);
        }
      };
      ```
