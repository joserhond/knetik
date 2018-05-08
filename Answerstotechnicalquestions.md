# Technical questions

1. How long did you spend on the coding test? What would you add to your solution if you had more time? If you didn't spend much time on the coding test then use this as an opportunity to explain what you would add.
*I spent around 6 hours. I would improve the pagination component and also add another component in order to let the user choose the number of devices displaying in each page of the pagination

2. What was the most useful feature that was added to the latest version of your chosen language? Please include a snippet of code that shows how you've used it.
*Use of simpler code with ES6. For example:
	created () {
    const vm = this
    axios.get('https://recruitment-test-api.devsandbox.knetikcloud.com/devices')
      .then((response) => {
        vm.devices = response.data.content
        vm.pages = response.data.total_pages
      }, (error) => {
        console.log(error)
      })
  }
In the code above there is no need to use the function keyword in the "created method" nor the promise of the http request

3. How would you track down a performance issue in production? Have you ever had to do this?
* I would analyze the source of the performance issue having the correct context of how and when the issue is happening. I track the times of the requests that are done in the app and check the code where necessary

4. How would you improve the Knetik APIs that you just used?
* I would add a path attribute to display a picture of the device. I would also create a filter for the signal attribute in order to get the devices between a range of values.
I would also add a post method to add more devices.

5. Please describe yourself using JSON.
{
	name: "José",
	lastname: "Rhon",
	age: 27,
	nationality: "Ecuadorian",
	main_qualities: [
		"responsible",
		"attentive",
		"careful",
		"calm",
		"easy going",
		"studious",
		"athlete"
	],
	education: [
		{
			level: "School",
			complete: true,
			name: "USA Academy",
			city: "Quito",
			country: "Ecuador"
		},
		{
			level: "High School",
			complete: true,
			name: "San Luis Gonzaga",
			city: "Quito",
			country: "Ecuador"
		},
		{
			level: "University",
			complete: true,
			name: "PUCE",
			city: "Quito",
			country: "Ecuador"
		},
		{
			level: "Master",
			complete: true,
			name: "Universidad Católica de Chile",
			city: "Santiago",
			country: "Chile"
		}
	],
	hobbies: [
		"play soccer",
		"watch soccer matches",
		"read news and stories about historical moments"
	],
	experience_technologies: [
		"PHP",
		"NodeJS",
		"C#",
		"AngularJS",
		"VueJS",
		"jQuery",
		"JavaScript",
		"SCSS",
		"CSS",
		"MongoDB",
		"MySQL",
		"SQL Server",
		"Git",
		"Bootstrap"
	]
}
