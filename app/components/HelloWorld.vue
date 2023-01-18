<template>
    <Page class="page" @loaded="onPageLoaded">
        <TabView :selectedIndex="activeTabIndex"
            @selectedIndexChange="onTabChange" selectedTabTextColor="#42B883"
            androidTabsPosition="bottom">
            <ActionBar title=" " flat="true"
                v-bind:class="{ completed: activeTabIndex == 1 }"></ActionBar>
            />

            <TabViewItem title="Main">
                <GridLayout columns="360, 300, auto,*"
                    rows="80, 80, 80, auto, auto, *">
                    <Label row="1" col="0"
                        text="Main, will select phase etc. Enric Codina"
                        class="list-entry" textWrap="true" />
                    <Label row="1" col="2" text="Database"
                        class="list-entry" />
                    <Label row="2" col="1" class="bold" :text="city"></Label>
                    <Label row="2" col="2" :text="summary"></Label>
                    <Label row="3" col="1" :text="day"></Label>
                    <Label row="4" col="1" :text="time"></Label>

                </GridLayout>
            </TabViewItem>

            <TabViewItem title="Flt Data Entry" :iconSource="todoIcon">
                <ScrollView orientation="vertical">
                    <GridLayout
                        rows="auto, auto, auto, 55, auto, auto, 55, auto, auto, auto, auto, auto, auto, auto, auto, auto, auto, auto,*"
                        columns="160, auto,*">
                        <Label row="0" class="header" text=" Flt Data" />
                        <Label row="2" class="list-entry" col="0"
                            text="Flt Number" />
                        <Label row="3" class="list-entry" col="0"
                            text="Date" />
                        <Label row="4" class="list-entry" text="Departure" />
                        <Label row="5" class="list-entry" col="0"
                            text="Destination" />
                        <Label row="6" class="list-entry" col="0"
                            text="ETD" />
                        <Label row="7" class="list-entry" col="0"
                            text="Flt Time" />
                        <Label row="8" class="list-entry" col="0"
                            text="Final Flt Lvl" />
                        <Label row="9" class="list-entry" col="0"
                            text="Acft Registration" />
                        <Label row="10" class="list-entry" col="0"
                            text="Gate" />
                        <Label row="11" class="list-entry" text="Loads" />
                        <Label row="12" class="list-entry" col="0"
                            text="FO" />
                        <Label row="13" class="list-entry" col="0"
                            text="Purser" />
                        <Label row="14" class="list-entry" col="0"
                            text="CSV Bus" />
                        <Label row="15" class="list-entry" col="0"
                            text="CSV Eco" />
                        <Label row="16" class="list-entry"
                            text="Augment CA" />
                        <Label row="17" class="list-entry" col="0"
                            text="Augment FO" />
                        <Label row="0" class="header" text="Entry" col="2" />

                        <TextField col="2" v-model="FltNbrValue" row="2"
                            hint="Flight number..." keyboardType="number"
                            returnKeyType="done"
                            @returnPress="onReturnPress" />

                        <DatePicker :year="currentYear" :month="currentMonth"
                            :day="currentDay" minDate="2019-01-01"
                            maxDate="2030-12-31" col="2" row="3"
                            v-model="selectedDate" />

                        <TextField ref="taskInput" v-model="DepartureValue"
                            row="4" col="2" hint="Departure..."
                            returnKeyType="done" autocorrect="false"
                            @returnPress="onReturnPress" />

                        <TextField ref="taskInput" v-model="DestinationValue"
                            row="5" col="2" hint="Destination..."
                            autocorrect="false" returnKeyType="done"
                            @returnPress="onReturnPress" />

                        <TimePicker :hour="currentHour"
                            :minute="currentMinute" @change="onChange" col="2"
                            row="6" minuteInterval="5"
                            @change="changeHandler" />
                        <TextField ref="taskInput" v-model="FtlTimeHourValue"
                            row="7" col="2" hint="HH:MM..."
                            returnKeyType="done" maxLength="5"
                            keyboardType="datetime"
                            @returnPress="onReturnPress" />
                        <TextField ref="taskInput" v-model="FltLvlValue"
                            row="8" keyboardType="number" col="2" hint="FL..."
                            maxLength="3" returnKeyType="done"
                            @returnPress="onReturnPress" />
                        <TextField ref="taskInput" v-model="AcftRegValue"
                            row="9" col="2" hint="A6-E..."
                            returnKeyType="done" maxLength="5"
                            autocorrect="false" keyboardType="capital"
                            @returnPress="onReturnPress" />
                        <TextField ref="taskInput" v-model="GateValue"
                            row="10" col="2" hint="Gate..."
                            returnKeyType="done" autocorrect="false"
                            @returnPress="onReturnPress" />
                        <TextField ref="taskInput" v-model="LoadsValue"
                            row="11" col="2" hint="Loads..."
                            returnKeyType="done"
                            @returnPress="onReturnPress" />
                        <TextField ref="taskInput" v-model="FONameValue"
                            row="12" col="2" hint="FO..." returnKeyType="done"
                            autocorrect="false"
                            @returnPress="onReturnPress" />
                        <TextField ref="taskInput" v-model="PurserNameValue"
                            row="13" col="2" hint="Purser..."
                            returnKeyType="done" autocorrect="false"
                            @returnPress="onReturnPress" />
                        <TextField ref="taskInput" v-model="CSVJNameValue"
                            row="14" col="2" hint="CSV Bus..."
                            returnKeyType="done" autocorrect="false"
                            @returnPress="onReturnPress" />
                        <TextField ref="taskInput" v-model="CSVYNameValue"
                            row="15" col="2" hint="CSV Eco..."
                            returnKeyType="done" autocorrect="false"
                            @returnPress="onReturnPress" />
                        <TextField ref="taskInput" v-model="AugCANameValue"
                            row="16" col="2" hint="Augment CA..."
                            autocorrect="false" returnKeyType="done"
                            @returnPress="onReturnPress" />
                        <TextField ref="taskInput" v-model="AugFONameValue"
                            row="17" col="2" hint="Augment FO..."
                            returnKeyType="done" autocorrect="false"
                            @returnPress="onReturnPress" />

                    </GridLayout>
                </ScrollView>
            </TabViewItem>

            <TabViewItem title="Timeline" :iconSource="todoIcon">
                <GridLayout rows="auto, auto, auto, auto, *"
                    columns="300, auto, auto, *">
                    <Label row="0" col="0" class="header" text="My Tasks" />
                    <Label row="0" col="1" class="header" text="ETD = " />
                    <Label row="0" col="2" class="header" text="04:40 Z" />
                    <TextView editable="false" row="0" col="3" class="header">
                        <FormattedString>
                            <Span>{{currentHour-4}}:{{currentMinute}} Z
                                {{currentMinute}}' to go</span>
                        </FormattedString>
                    </TextView>
                    <ListView row="2" class="list-group" for="todo in todos"
                        itemLoading="onItemLoading">
                        <v-template>
                            <GridLayout columns="auto, *" class="list-entry">
                                <Label col="0"
                                    v-on:tap="onTodoCircleTap(todo)"
                                    class="circle" text=" " />
                                <Label col="1" v-on:tap="onTodoItemTap(todo)"
                                    :text="todo.name" textWrap="true" />
                            </GridLayout>
                        </v-template>
                    </ListView>
                </GridLayout>
            </TabViewItem>

            <TabViewItem title="Completed" :iconSource="completedIcon">
                <GridLayout rows="auto, *">
                    <Label row="0" class="header completed"
                        text="Completed Tasks" />

                    <ListView row="1" class="list-group" for="done in dones"
                        itemLoading="onItemLoading">
                        <v-template>
                            <GridLayout columns="auto, *"
                                class="list-entry list-entry-completed">
                                <Label col="0"
                                    v-on:tap="onCompletedCircleTap(done)"
                                    class="circle" text="✓" />
                                <Label col="1"
                                    v-on:tap="onCompletedItemTap(done)"
                                    :text="done.name" textWrap="true" />
                            </GridLayout>
                        </v-template>
                    </ListView>
                </GridLayout>
            </TabViewItem>

            <TabViewItem title="Fuel">
                <GridLayout
                    rows="auto, auto,auto, auto, auto, auto,auto, auto, auto, auto, auto, auto, auto, auto, auto,*"
                    columns="auto,*"class="TextField" fontSize="18">
                    <Label row="0" class="header completed" text="Fuel" />
                    <Label row="2" col="0" text=" "
                        class="TextField" />
                    <Label row="1" col="0"
                        text="ZFW changes, Turnaround fuel, Techlog gross error, "
                         />
                    <Label row="3" col="0" text="EZFW"
                        class="list-entry list-entry-completed" />
                    <Label row="4" col="0" text="AZFW"
                        class="list-entry list-entry-completed" />
                    <Label row="5" col="0" text="ZFW change"
                        class="list-entry list-entry-completed" />
                    <Label row="6" col="0" text="Trip change"
                        class="list-entry list-entry-completed" />
                    <Label row="7" col="0" text="Extra fuel over destination"
                        class="list-entry list-entry-completed" />
                    <Label row="8" col="0" text="Total extra fuel"
                        class="list-entry list-entry-completed" />
                    <Label row="9" col="0" text="New TO Fuel"
                        class="list-entry list-entry-completed" />
                    <Label row="10" col="0" text="Taxi Out"
                        class="list-entry list-entry-completed" />
                    <Label row="11" col="0" text="Ramp Fuel"
                        class="list-entry list-entry-completed" />
                    <Label row="12" col="0" text="Trip"
                        class="list-entry list-entry-completed" />
                    <Label row="13" col="0"
                        text="TOW:      LW:     OvW:      MLF:     JettTime:    "
                        class="list-entry list-entry-completed" />

                    <Label row="0" col="1" class="header completed" />
                    <Label row="1" col="1" text="TurnAround"
                        class="list-entry list-entry-completed" />
                    <Label row="2" col="1" text=" "
                        class="list-entry list-entry-completed" />
                    <Label row="3" col="1" text="Time on ground"
                        class="list-entry list-entry-completed" />
                    <Label row="4" col="1" text="Return Fuel"
                        class="list-entry list-entry-completed" />
                    <Label row="5" col="1" text="Return addnl"
                        class="list-entry list-entry-completed" />
                    <Label row="6" col="1" text="Taxi in 1st sector"
                        class="list-entry list-entry-completed" />
                    <Label row="7" col="1" text="Trip 1st sector"
                        class="list-entry list-entry-completed" />
                    <Label row="8" col="1" text="Taxi out 1st sector"
                        class="list-entry list-entry-completed" />
                </GridLayout>
            </TabViewItem>

            <TabViewItem title="PA">
                <ScrollView orientation="vertical">
                    <GridLayout
                        rows="auto, auto, auto, auto, auto, auto, auto, auto, auto, auto, auto, auto, auto, auto, *"
                        width="auto">
                        <Label text="Welcome PA" row="0" class="header">
                        </Label>
                        <Label row="1" textWrap="true" backgroundColor="white"
                            fontSize="24">
                            <Span
                                text="Good morning Ladies and Gentlemen, this is the Captain speaking, my name is Enric Codina and I am from Barcelona. Joining me in the flight deck Senior First Officer " />
                            <Span> {{FONameValue}} </span>
                            <Span
                                text=" from ... , our cabin crew led by the Purser " />
                            <Span> {{PurserNameValue}} </span>
                            <Span text=" from ... , and Cabin Supervisors " />
                            <Span> {{CSVJNameValue}} </span>
                            <Span
                                text=" from ... in Business section and  " />
                            <Span> {{CSVYNameValue}} </span>
                            <Span text=" from ... in Economy section." />
                        </Label>
                        <Label row="2" textWrap="true" backgroundColor="white"
                            fontSize="24">
                            <Span
                                text="It is our pleasure to welcome you on board Emirates flight " />
                            <Span> {{FltNbrValue}} </span>
                            <Span text=" to " />
                            <Span> {{DestinationValue}} </span>
                            <Span
                                text=". Our route today is via ... , ..., ... The planned flight time is " />
                            <Span> {{FtlTimeHourValue}} </span>
                            <Span text=" hours and " />
                            <Span> {{FltTimeMinValue}} </span>
                            <Span
                                text=" minutes with a final cruising altitude of " />
                            <Span> {{FltLvlValue}} </span>
                            <Span
                                text="  feet. You can follow our progress on the sky show channel of your video screen." />
                        </Label>
                        <Label row="3" textWrap="true" backgroundColor="white"
                            fontSize="24">
                            <Span
                                text="The forecasted enroute weather is expected to be mainly smooth, and destination weather will be..." />
                            <Span
                                text="As always for your own safety, please keep your seat belts fastened at all times when seated, just in case we encounter any unexpected bumps. I would like to remind you all emirates flights are non smoking flights." />
                        </Label>
                        <Label row="4" textWrap="true" backgroundColor="white"
                            fontSize="24">
                            <Span
                                text="We are now completing the last paperwork and expect to depart shortly. Please relax and enjoy our award winning inflight service. We will update you with the arrival details just prior to the descent. Thank you." />
                        </Label>
                        <Label row="5" textWrap="true"
                            backgroundColor="white">
                            <Span text=" " />
                        </Label>
                        <Label row="6" textWrap="true" backgroundColor="white"
                            fontSize="24">
                            <Span
                                text="COVID PA:   Due the current COVID pandemic, I must also remind you to wear your face masks whenever possible." />
                        </Label>
                        <Label row="7" textWrap="true"
                            backgroundColor="white">
                            <Span text=" " />
                        </Label>
                        <Label row="8" textWrap="true"
                            backgroundColor="white">
                            <Span text=" " />
                        </Label>
                        <Label row="9" textWrap="true" backgroundColor="white"
                            fontSize="24">
                            <Span
                                text="Deice PA:   Ladies and gentlemen, this is the captain. Due to the current weather the ground crew will be spraying de-icing fluid on the aircraft before we depart. This process is about to start now and will take approximately 10 minutes. As soon as the process is completed, we'll be ready for departure. Thank you for your patience." />
                        </Label>
                        <Label row="10" textWrap="true"
                            backgroundColor="white">
                            <Span text=" " />
                        </Label>
                        <Label row="11" textWrap="true"
                            backgroundColor="white" fontSize="24">
                            <Span
                                text="Delay PA:   Ladies and gentlemen, this is the captain. Air Traffic Control has just advised us that due to (congestion, runway closure, maintenance,...) we can expect a delay of approximately XX minutes before we are able to depart. Thank you for your patience and understanding." />
                        </Label>
                        <Label row="12" textWrap="true"
                            backgroundColor="white">
                            <Span text=" " />
                        </Label>
                        <Label row="13" textWrap="true"
                            backgroundColor="white" fontSize="24">
                            <Span
                                text="USA PA:   Ladies and gentlemen, US Regulations require me to inform you that during this flight today, you should not congregate in groups in any area of the cabin especially around lavatories. I would also ask you to use only those lavatories dedicated to your class of service. Also, you must strictly observe the seat belt sign when it is illuminated and do not move about the cabin when the sign is on. Thank you" />
                        </Label>

                    </GridLayout>
                </ScrollView>
            </TabViewItem>

            <TabViewItem title="FTL">
                <Label text=" Flight Time Limitations calculator"
                    textWrap="true" />
            </TabViewItem>
        </TabView>
    </Page>
</template>

<script>
    const platform = require("tns-core-modules/platform");
    const frame = require("tns-core-modules/ui/frame");
    const Geolocation = require("nativescript-geolocation");
    const Accuracy = require("tns-core-modules/ui/enums");
    const http = require("tns-core-modules/http");

    export default {
        onPageLoaded() {
            if (platform.isIOS) {
                const navBar = frame.topmost().ios.controller.navigationBar;
                navBar.barStyle = UIBarStyle.UIBarStyleBlack;
                IQKeyboardManager.sharedManager().enableAutoToolbar = false;
            }
        },
        onItemLoading(args) {
            if (args.ios) {
                args.ios.selectionStyle = UITableViewCellSelectionStyle.None;
            }
        },
        methods: {
            /*      changeHandler(eventData) {
                                                                                                                                                                                                                                                                                                                                                                                                        eventData - > {
                                                                                                                                                                                                                                                                                                                                                                                                            data: {
                                                                                                                                                                                                                                                                                                                                                                                                                HH: ...,
                                                                                                                                                                                                                                                                                                                                                                                                                mm: ...
                                                                                                                                                                                                                                                                                                                                                                                                            },
                                                                                                                                                                                                                                                                                                                                                                                                            displayTime: 'HH:mm'
                                                                                                                                                                                                                                                                                                                                                                                                        }
                                                                                                                                                                                                                                                                                                                                                                                                    },*/
            onTodoItemTap(item) {
                const index = this.todos.indexOf(item);
                action("What do you want to do with this task?", "Cancel", [
                    "Mark completed",
                    "Delete forever"
                ]).then(result => {
                    console.log(result);
                    switch (result) {
                        case "Mark completed":
                            this.dones.unshift(item);
                            this.todos.splice(index, 1);
                            break;
                        case "Delete forever":
                            this.todos.splice(index, 1);
                            break;
                        case "Cancel" || undefined:
                            break;
                    }
                });
            },
            onTodoCircleTap(item) {
                const index = this.todos.indexOf(item);
                this.dones.unshift(item);
                this.todos.splice(index, 1);
            },
            onCompletedItemTap(item) {
                const index = this.dones.indexOf(item);
                action("What do you want to do with this task?", "Cancel", [
                    "Mark to do",
                    "Delete forever"
                ]).then(result => {
                    console.log(result);
                    switch (result) {
                        case "Mark to do":
                            this.todos.unshift(item);
                            this.dones.splice(index, 1);
                            break;
                        case "Delete forever":
                            this.dones.splice(index, 1);
                            break;
                        case "Cancel" || undefined:
                            break;
                    }
                });
            },
            onCompletedCircleTap(item) {
                const index = this.dones.indexOf(item);
                this.todos.unshift(item);
                this.dones.splice(index, 1);
            },

            onReturnPress() {
                if (this.textFieldValue.trim() === "") {
                    this.$refs.taskInput.nativeView.focus();
                    return;
                }

                console.log("New task added: " + this.textFieldValue + ".");
                this.todos.unshift({
                    name: this.textFieldValue
                });
                this.textFieldValue = "";
            },

            onTabChange(tab) {
                this.activeTabIndex = tab.value;
            },
            getMyWeather() {
                Geolocation.enableLocationRequest();
                Geolocation.getCurrentLocation({
                    desiredAccuracy: Accuracy.high,
                    updateDistance: 0.1,
                    timeout: 20000
                }).then(
                    loc => {
                        if (loc) {
                            var appId =
                            "6a762036bad9d1ec55fa6fb322d16a5e";
                            var url =
                                "https://api.openweathermap.org/data/2.5/weather?APPID=" +
                                appId +
                                "&units=metric&lat=" +
                                loc.latitude +
                                "&lon=" +
                                loc.longitude;
                            http.request({
                                url: url,
                                method: "GET"
                            }).then(this.parseResponse);
                        }
                    },
                    function(e) {
                        console.log("Error: " + e.message);
                    }
                );
            },
            parseResponse(response) {
                var location = response.content.toJSON();
                this.city = location.name;
            }
        },
        data() {
            return {
                currentDay: new Date().getUTCDate(),
                currentMonth: new Date().getUTCMonth() + 1,
                currentYear: new Date().getUTCFullYear(),

                currentHour: new Date().getHours(),
                currentMinute: new Date().getMinutes(),

                destinations: [{
                        name: "Dubai"
                    },
                    {
                        name: "New Delhi"
                    },
                    {
                        name: "Tehran"
                    },
                    {
                        name: "Hungary",
                        imageSrc: "https://play.nativescript.org/dist/assets/img/flags/hu.png"
                    },
                    {
                        name: "United States",
                        imageSrc: "https://play.nativescript.org/dist/assets/img/flags/us.png"
                    }
                ],

                todos: [{
                        name: "Egate opens"
                    },
                    {
                        name: "Pickup"
                    },
                    {
                        name: "CC Brief starts"
                    },
                    {
                        name: "Flt Crew Brief starts"
                    },
                    {
                        name: "Joint Brief starts"
                    },
                    {
                        name: "Joint Brief ends"
                    },
                    {
                        name: "Bus departs"
                    },
                    {
                        name: "Latest onboard"
                    },
                    {
                        name: "Remote/Autoboard"
                    },
                    {
                        name: "Walk around"
                    },
                    {
                        name: "OPT"
                    },
                    {
                        name: "FZFW DXB"
                    },
                    {
                        name: "FZFW Outstation"
                    },
                    {
                        name: "Send Fuel Figures"
                    },
                    {
                        name: "ATC Clearance"
                    },
                    {
                        name: "Briefing"
                    },
                    {
                        name: "Preflight XL"
                    },
                    {
                        name: "Notoc"
                    },
                    {
                        name: "Loadsheet"
                    },
                    {
                        name: "Accept Loadsheet"
                    },
                    {
                        name: "CDU Data Entry"
                    },
                    {
                        name: "MCP"
                    },
                    {
                        name: "APU"
                    },
                    {
                        name: "Offloading bags"
                    },
                    {
                        name: "Techlog sign, Cabin log"
                    },
                    {
                        name: "Security Form"
                    },
                    {
                        name: "Tug"
                    },
                    {
                        name: "PA"
                    },
                    {
                        name: "Doors closed"
                    }
                ],
                dones: [],
                textFieldValue: "",
                activeTabIndex: 0,
                todoIcon: platform.isIOS ? "~/./images/To-Do@3x.png" : "",
                completedIcon: platform.isIOS ?
                    "~/./images/Completed@3x.png" : ""
            };
        },
        created() {
            this.getMyWeather();
            var currentDate = new Date();
            var day = currentDate.getDay();
            var weekdays = new Array(7);
            weekdays[0] = "Sunday";
            weekdays[1] = "Monday";
            weekdays[2] = "Tuesday";
            weekdays[3] = "Wednesday";
            weekdays[4] = "Thursday";
            weekdays[5] = "Friday";
            weekdays[6] = "Saturday";
            var dayName = weekdays[day];
            var currentHours = currentDate.getHours();
            var timeOfDay = currentHours >= 12 ? "Afternoon" : "Morning";
            this.day = dayName;
            this.time = timeOfDay;
        }
    };
</script>

<style scoped>
    ActionBar {
        background-color: #35495E;
    }

    .header {
        background-color: #B22222;
        color: white;
        font-size: 34;
        font-weight: 600;
        padding: 0 15 15 15;
        margin: 0;
    }

    .completed {
        background-color: #B22222;
    }

    TextField {
        width: 100%;
        font-size: 17;
        color: black;
        placeholder-color: #8B0000;
        padding: 17;
        border-width: 0 0 1 0;
        border-color:
            #E0E0E0;
    }

    .list-entry {
        padding: 0 15;
        color: #42B883;
    }

    .circle {
        width: 30;
        height: 30;
        padding: 0;
        color: #42B883;
        font-size: 25;
        border-color: #42B883;
        border-width: 2;
        border-radius:
            50;
    }

    .list-entry .circle {
        margin: 0 10 0 0;
    }

    .list-entry Label {
        font-weight: bold;
        font-size: 17;
        vertical-align: middle;
        padding: 17 0;
        margin: 0;
    }

    .list-entry-completed .circle {
        color: white;
        background-color: #42B883;
        text-align: center;
        padding: 0;
            }
</style>
