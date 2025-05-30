public class Event
{
    public string Name { get; set; }
    public DateTime Date { get; set; }
    public string Location { get; set; }
    public string Description { get; set; }
    public List<string> Tasks { get; set; } = new List<string>();
}

@page "/eventease"

<h3>EventEase - Event Manager</h3>

<label>Event Name:</label>
<input @bind="Event.Name" />

<label>Date:</label>
<input type="date" @bind="Event.Date" />

<label>Location:</label>
<input @bind="Event.Location" />

<label>Description:</label>
<textarea @bind="Event.Description"></textarea>

<h4>Tasks</h4>
<input @bind="NewTask" />
<button @onclick="AddTask">Add Task</button>

<ul>
    @foreach (var task in Event.Tasks)
    {
        <li>@task <button @onclick="() => RemoveTask(task)">❌</button></li>
    }
</ul>

<button @onclick="SaveEvent">Save Event</button>

@code {
    private Event Event = new Event();
    private string NewTask;

    private void AddTask()
    {
        if (!string.IsNullOrWhiteSpace(NewTask))
        {
            Event.Tasks.Add(NewTask);
            NewTask = "";
        }
    }

    private void RemoveTask(string task)
    {
        Event.Tasks.Remove(task);
    }

    private void SaveEvent()
    {
        Console.WriteLine("Event Saved: " + Event.Name);
    }
}

<Router AppAssembly="@typeof(Program).Assembly">
    <Found>
        <RouteView />
    </Found>
</Router>
