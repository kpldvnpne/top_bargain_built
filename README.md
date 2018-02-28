# top_bargain_built
Production ready build files for the front end

Some changes need to be made within <code>index.html</code> file. Refer to this site for more info:
https://docs.djangoproject.com/en/2.0/howto/static-files/

The web app makes AJAX requests to the servers. Some of the requests it makes for now are listed below:

<h2>1. Login</h2>
<p>During login, after submission, a <code>POST</code> request is made to the server, with following settings</p>
<ul>
  <li>URL: '/login'</li>
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
  <li>URL: '/instantSearch'</li>
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
  <li>URL: '/search'</li>
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
<p style="background: red; color: white;">Not working properly. Ignore this part for now. For data, create fake ones for now.</p>
<ul>
  <li>URL: '/post'</li>
  <li>Method: <code>POST</code></li>
  <li>A request containing a JSON object like following is sent:
  <pre>
    {
      personname: "Person Name",
      product: "Towel",
      price: 300,
      location: "Baneshwor",
      file: Image File                //Ignore this for now
    }
  </pre>
  </li>
  <li>Required response: A JSON object that shows whether the post was successfully posted or not. It looks like following
    <pre>
      {
        success: "yes"              //Depends on success
      }
    </pre>
  </li>
</ul>
