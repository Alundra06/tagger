Tagger
===============================================================

Tagger is a fluid Html tag builder that supports Html creation in a compile safe and testable way.

Installation available on NuGet [http://nuget.org/packages/Tagger/](http://nuget.org/packages/Tagger/)

### Basic usages

	var div = new Div()
				.Class("input-wrap")
				.Add(new Label()
						.For("email")
						.Text("Email Address:")
				)
				.Add(new Input()
						.Id("email")
						.Name("email")
						.Class("required")
						.AddClass("email")
				);

#### Call `div.GetHtml()` or `div.ToString()` to get the html output

	<div class="input-wrap">
		<label for="email">Email Address:</label>
		<input type="textbox" id="email" name="email"></input>
	</div>

#### Adding multiple tags using parameters

	var div = new Div()
				.Add(
					new Span().Text("Option 1"),
					new Span().Text("Option 2"),
					new Span().Text("Option 3")
				);
	<div>
		<span>Option 1</span>
		<span>Option 2</span>
		<span>Option 3</span>
	</div>

#### Surrounding tags

	var button = new Button(ButtonType.Button)
					.SurroundWith(new Form());

	<form>
		<button type="button"></button>
	</form>
					
#### Void tags

	var tag = new HtmlTag("hr").SelfClose();

	<hr />

### Form elements

Some form elements have special usage

#### Select lists

	var tag = new Select()
				.Add(
					new Option().Text("Option 1").Value("1"),
					new Option().Text("Option 2").Value("2"),
					new Option().Text("Option 3").Value("3")
				);
	<select>
		<option value="1">Option 1</option>
		<option value="2">Option 2</option>
		<option value="3">Option 3</option>
	</select>

#### Select lists using `KeyValuePair<string, string>`

	var options = new Dictionary<string, string>();
	options.Add("1", "Option 1");
	options.Add("2", "Option 2");
	options.Add("3", "Option 3");

	var tag = new Select().Add(options);

	<select>
		<option value="1">Option 1</option>
		<option value="2">Option 2</option>
		<option value="3">Option 3</option>
	</select>

### Tables

Tables follow the same basic usage, but have a couple helper methods for quick table creation.

Simple tables that only contain string text can be created like this:

	var table = new Table()
        .Add(new TableRow(new TableCell("Apples"), new TableCell("Oranges")));

Shortcut method that does the same thing as the above statement:

	var table = new Table()
        .AddRow("Apples", "Oranges", "Bananas");

More complex tables with headers and footers

	var table = new Table()
        .Add(new TableHeader()
                 .Add(new TableRow(new TableHeaderCell("Id"), new TableHeaderCell("Name"))
                 )
        ).Add(new TableBody()
                  .Add(new TableRow(new TableCell("1234"), new TableCell("Apples"))
                  )
        ).Add(new TableFooter()
                  .Add(new TableRow(new TableCell("Id"), new TableCell("Name"))
                  )
        );