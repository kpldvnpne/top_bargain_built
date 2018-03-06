# top_bargain_built
Production ready build files for the front end

Some changes need to be made within <code>index.html</code> file. Refer to this site for more info:
https://docs.djangoproject.com/en/2.0/howto/static-files/

The web app makes AJAX requests to the servers. Some of the requests it makes for now are listed below:

<h2>1. Login</h2>
<p>During login, after submission, a <code>POST</code> request is made to the server, with following settings</p>
<ul>
  <li>URL: <code>'/login'</code></li>
  <li>Method: <code>POST</code></li>
  <li>JSON Object: Contains username and password
  <pre>
    {
      username: "username",
      password: "password",
    }
  </pre>
  </li>
  <li>Required response: A JSON that looks like following
    <pre>
      {
        loggedIn: "yes",        //If login was successful
      }
    </pre>
  </li>
</ul>

<h2>2. Instant Search</h2>
<p>When typing in to search the items available, this AJAX request requests the server for relevent search results</p>
<ul>
  <li>URL: <code>'/instantSearch'</code></li>
  <li>Method: <code>GET</code></li>
  <li>This get method contains only one query item:
  <pre>
    q = "input_query"       //What is being typed is being sent every time to the server
  </pre>
  </li>
  <li>Required response: A JSON object that looks like following
    <pre>
      {
        instantSearchList: [          //This means it contains an array
          "Table",
          "Radio",
          "Item_3",
          "Item_4",
          "As many as you like",
          "But must be a string"
        ]
      }
    </pre>
  </li>
</ul>

<h2>3. Main Search</h2>
<p>After finished typing and pressing enter, the item entered into the search input is sent asynchronously.</p>
<ul>
  <li>URL: <code>'/search'</code></li>
  <li>Method: <code>GET</code></li>
  <li>This get method contains only one query item:
  <pre>
    q = "input_query"       //What is being typed is sent to the server after pressing enter
  </pre>
  </li>
  <li>Required response: A JSON object that looks like following
    <pre>
      {
        searchResults: {
          recommendedPrice: 1000,               //tl;dr It should contain a recommended price, returned by the system as well as
          list: [                               //a list containing relevant search results
            {
              image: new Blob(),
              productName: "Table",
              location: "Baneshwor",
              price: 1500
            },
            {
              image: new Blob(),
              productName: "Table",
              location: "Baneshwor",
              price: 1500
            },
          ]
        },
      };
    </pre>
  </li>
</ul>

<h2>4. Posting of an item</h2>
<p>After entering an item, and hitting submit, the entered info is sent by AJAX to the server. The configuration of this AJAX request is </p>
<ul>
  <li>URL: <code>'/post'</code></li>
  <li>Method: <code>POST</code></li>
  <li>A request containing a JSON object like following is sent:
  <pre>
    {
      productName: "Towel",
      price: 300,
      location: "Baneshwor",
      productImage: imageFile     //The image of file would be here
    }
  </pre>
  </li>
  <li>
    To know how to read the productImage in the Django Backend, confer the following link:
    <a href="https://stackoverflow.com/questions/33182517/django-how-can-i-get-each-file-in-formdata-when-i-use-ajax-to-send-to-the-serv">Read image from FormData in Django Backend</a>
  </li>
  <li>Required response: Any response could be sent. The output would appear as below, for which you have to check console.
    <pre>
      "Response after posting porduct" + theResponseSentFromBackend
    </pre>
  </li>
</ul>
