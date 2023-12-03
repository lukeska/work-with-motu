<script setup>
import { onMounted, ref } from "vue";
import { TransitionRoot } from "@headlessui/vue";
import { roundCorners } from "svg-round-corners";
import Button from "./components/Button.vue";

let button1 = ref();
let button2 = ref();
let button3 = ref();
let button4 = ref();
let button5 = ref();

let box = ref();
let selectedButton = ref("button3");

const mastersOfTheUniver = [
	{
		button: "button1",
		name: "Evil Lynn",
		location: "A mysterious and ancient sorcerer's lair",
		bio: "Evil-Lyn, sorceress extraordinaire! Mistress of dark magic, strategic brilliance, and occasional eye-rolling at Skeletor's plans. Embracing the shadows, I command the arcane forces to achieve our wicked goals. Join me in the pursuit of power, secrets, and the occasional sinister chuckle. Beware, for chaos and cunning are my allies. #EvilLyn #MistressOfMagic #Sorceress",
		pic: "/work-with-motu/evil-lynn.jpg",
		skills: [
			{ name: "Sorcery", value: "10/10" },
			{ name: "Manipulation", value: "9/10" },
			{ name: "Intelligence", value: "8/10" },
			{ name: "Ambition", value: "8/10" },
			{ name: "Mystical Knowledge", value: "9/10" },
		],
	},
	{
		button: "button2",
		name: "Skeletor",
		location: "Snake Mountain",
		bio: "Skeletor, the cackling overlord of evil! Master of mischief, aspiring conqueror, and eternal rival to He-Man. Unleashing chaos and sarcasm in equal measure. Join me on this twisted journey through Snake Mountain, where every day is a scheme to rule Eternia. Fear me, mortals, as I command the forces of darkness and revel in the chaos of villainy! #SkeletorLaughsLast #EvilOverlord",
		pic: "/work-with-motu/skeletor.jpg",
		skills: [
			{ name: "Dark Magic", value: "10/10" },
			{ name: "Intelligence", value: "9/10" },
			{ name: "Ambition", value: "8/10" },
			{ name: "Cunning", value: "8/10" },
			{ name: "Command of Evil Forces", value: "9/10" },
		],
	},
	{
		button: "button3",
		name: "He-Man",
		location: "Castle Grayskull",
		bio: "He-Man, the mighty wielder of the Power of Grayskull! Defender of Eternia, master of the universe, and all-around hero. By the power of Twitter, I share wisdom, courage, and a touch of humor. Join me on my adventures as we battle Skeletor, explore Castle Grayskull, and celebrate the triumph of good over evil. #ByThePowerOfTwitter #HeMan #CastleGrayskull",
		pic: "/work-with-motu/he-man.jpg",
		skills: [
			{ name: "Strength", value: "11/10" },
			{ name: "Endurance", value: "9/10" },
			{ name: "Courage", value: "8/10" },
			{ name: "Leadership", value: "8/10" },
			{ name: "Mastery of the Power", value: "9/10" },
		],
	},
	{
		button: "button4",
		name: "Teela",
		location: "Royal Palace",
		bio: "Teela, fearless warrior of Eternia! Captain of the Royal Guard, defender of Castle Grayskull, and loyal ally to He-Man. Embracing strength, honor, and a touch of sarcasm. Join me on the front lines as we stand against the forces of evil. Training hard, fighting harder, and always ready for the next adventure! #Teela #RoyalGuard #RoyalPalace #StrengthAndHonor",
		pic: "/work-with-motu/teela.jpg",
		skills: [
			{ name: "Combat Skill", value: "10/10" },
			{ name: "Agility", value: "9/10" },
			{ name: "Loyalty", value: "8/10" },
			{ name: "Tactical Insight", value: "8/10" },
			{ name: "Leadership Potential", value: "9/10" },
		],
	},
	{
		button: "button5",
		name: "Orko",
		location: "Trolla",
		bio: "Orko, the magical mischief-maker! Jovial jester from Trolla, spreading laughter and unintentional chaos. Join me on my whimsical adventures, where spells go awry, and pranks abound. Despite the mishaps, my heart is pure, and I'm always ready to lend a helping hand. Let's navigate the ups and downs with a smile and a bit of magic! #Orko #TrollanMagic #KeepSmiling",
		pic: "/work-with-motu/orko.jpg",
		skills: [
			{ name: "Magic Proficiency", value: "10/10" },
			{ name: "Playfulness", value: "9/10" },
			{ name: "Kindness", value: "8/10" },
			{ name: "Mischievousness", value: "8/10" },
			{ name: "Innate Goodness", value: "9/10" },
		],
	},
];

onMounted(() => {
	const bodyElement = document.body;

	resizeObserver.observe(bodyElement);

	initCurveConnections();
});

const initCurveConnections = () => {
	drawCurveConnection("button1", button1);
	drawCurveConnection("button2", button2);
	drawCurveConnection("button3", button3);
	drawCurveConnection("button4", button4);
	drawCurveConnection("button5", button5);
};

const drawCurveConnection = (buttonName, buttonStart) => {
	const stroke = 1;
	let strokeColor = "white";
	let opacity = "opacity-20";

	const rect1 = buttonStart.value.$el.getBoundingClientRect();
	const rect2 = box.value.getBoundingClientRect();
	const xDiff = rect2.x - rect1.x;
	const yDiff = rect2.y - rect1.height - rect1.y;

	const xStart = rect1.width / 2 + stroke / 2;

	// define path for small screens
	let svgPathData = `m${xStart + 640},${rect1.height}l0,${yDiff / 2}l${
		xDiff - rect1.width / 2 + rect2.width / 2
	},0l0.0001,${yDiff / 2}`; // the last 0.0001 is a hack to prevent linear gradient to have the line disappear if it's perfectly straight

	let viewportWidth =
		window.innerWidth || document.documentElement.clientWidth;

	// redefine path for large screens
	if (viewportWidth >= 1280) {
		svgPathData = `m${rect1.width},${rect1.height / 2 + 300}l${
			(rect2.x - rect1.x - rect1.width) / 2
		},0l0,${
			rect2.height / 2 - rect1.y + rect1.height + 8 - window.scrollY
		}l${(rect2.x - rect1.x - rect1.width) / 2},0.0001`;
	}

	// Specify the radius for rounding the corners
	const cornerRadius = 20;

	// Round the corners of the SVG path
	const roundedPathData = roundCorners(svgPathData, cornerRadius);

	// Create an SVG element
	const svgElement = document.createElementNS(
		"http://www.w3.org/2000/svg",
		"svg"
	);
	svgElement.setAttribute("width", 1280);
	svgElement.setAttribute("height", 600);

	if (buttonName == selectedButton.value) {
		// Create a linear gradient
		var linearGradient = document.createElementNS(
			"http://www.w3.org/2000/svg",
			"linearGradient"
		);
		linearGradient.setAttribute("id", "grad1");

		if (viewportWidth >= 1280) {
			// horizontal gradient
			linearGradient.setAttribute("x1", "0%");
			linearGradient.setAttribute("y1", "0%");
			linearGradient.setAttribute("x2", "100%");
			linearGradient.setAttribute("y2", "0%");
		} else {
			// vertical gradient
			linearGradient.setAttribute("x1", "0%");
			linearGradient.setAttribute("y1", "0%");
			linearGradient.setAttribute("x2", "0%");
			linearGradient.setAttribute("y2", "100%");
		}

		// Create gradient stops
		var stop1 = document.createElementNS(
			"http://www.w3.org/2000/svg",
			"stop"
		);
		stop1.setAttribute("offset", "0%");
		stop1.style.stopColor = "#d4a68b";
		stop1.style.stopOpacity = 1;
		linearGradient.appendChild(stop1);

		var stop2 = document.createElementNS(
			"http://www.w3.org/2000/svg",
			"stop"
		);
		stop2.setAttribute("offset", "100%");
		stop2.style.stopColor = "#c07fea";
		stop2.style.stopOpacity = 1;
		linearGradient.appendChild(stop2);

		// Append the linear gradient to the defs
		var defs = document.createElementNS(
			"http://www.w3.org/2000/svg",
			"defs"
		);
		defs.appendChild(linearGradient);

		svgElement.appendChild(defs);

		strokeColor = "url(#grad1)";
		opacity = "opacity-100";
	}

	// Create an SVG path element
	let solidPath;

	solidPath = getPath(roundedPathData.path, stroke, strokeColor, opacity);
	svgElement.appendChild(solidPath);

	// Append the SVG element to the HTML document
	let svgContainer = buttonStart.value.$el.querySelector(".svg-container");
	svgContainer.innerHTML = "";
	svgContainer.appendChild(svgElement);
};

const getPath = (path, strokeWidth, strokeColor, opacity) => {
	const pathElement = document.createElementNS(
		"http://www.w3.org/2000/svg",
		"path"
	);

	pathElement.setAttribute("class", opacity);

	pathElement.setAttribute("d", path);
	pathElement.setAttribute("stroke", strokeColor);
	pathElement.setAttribute("stroke-width", strokeWidth);
	pathElement.setAttribute("stroke-linecap", "round");
	pathElement.setAttribute("fill", "none");

	return pathElement;
};

const resizeObserver = new ResizeObserver((entries) => {
	for (const entry of entries) {
		initCurveConnections();
	}
});

const setActiveButton = (buttonName) => {
	selectedButton.value = buttonName;

	initCurveConnections();
};
</script>

<template>
	<div class="h-full overflow-x-clip">
		<div class="container px-4 py-10 mx-auto md:py-20">
			<div
				class="mb-16 xl:w-2/3 xl:pl-[33%] xl:text-left text-center text-transparent bg-clip-text bg-gradient-to-r from-white via-50% via-[#efe4b9] to-75% to-[#dd9cbe]"
			>
				Work with your soon-to-be favorite Master of the Universe.
			</div>
			<div class="xl:flex">
				<div
					class="flex justify-between mb-24 xl:mb-0 xl:w-1/3 xl:flex-col xl:gap-y-10 xl:justify-center"
				>
					<Button
						img="/work-with-motu/evil-lynn.jpg"
						ref="button1"
						@click.prevent="setActiveButton('button1')"
						:active="selectedButton == 'button1'"
						>Evil Lynn</Button
					>
					<Button
						img="/work-with-motu/skeletor.jpg"
						ref="button2"
						@click.prevent="setActiveButton('button2')"
						:active="selectedButton == 'button2'"
						>Skeletor</Button
					>
					<Button
						img="/work-with-motu/he-man.jpg"
						ref="button3"
						@click.prevent="setActiveButton('button3')"
						:active="selectedButton == 'button3'"
						>He-Man</Button
					>
					<Button
						img="/work-with-motu/teela.jpg"
						ref="button4"
						@click.prevent="setActiveButton('button4')"
						:active="selectedButton == 'button4'"
						>Teela</Button
					>
					<Button
						img="/work-with-motu/orko.jpg"
						ref="button5"
						@click.prevent="setActiveButton('button5')"
						:active="selectedButton == 'button5'"
						>Orko</Button
					>
				</div>
				<div
					ref="box"
					class="gradient-border box-gradient-border max-w-[700px] mx-auto xl:max-w-none xl:w-2/3 px-6 md:px-24 py-12 border border-transparent rounded-3xl flex-1 ring-[10px] ring-[#232436] outline outline-[10px] outline-[#19192b] outline-offset-[10px]"
				>
					<template
						v-for="master in mastersOfTheUniver"
						:key="master.name"
					>
						<div
							v-if="master.button == selectedButton"
							class="box-content relative z-40 space-y-10"
						>
							<div class="flex items-center space-x-4">
								<img
									:src="master.pic"
									:alt="master.name"
									class="w-10 h-10 rounded-full"
								/>
								<h2 class="text-2xl font-black">
									{{ master.name }}
								</h2>
							</div>
							<div>
								<div class="mb-3 font-bold text-indigo-100">
									Location
								</div>
								<div class="text-slate-400">
									{{ master.location }}
								</div>
							</div>
							<div>
								<div class="mb-3 font-bold text-indigo-100">
									Description
								</div>
								<div class="text-slate-400">
									{{ master.bio }}
								</div>
							</div>
							<div>
								<div class="mb-3 font-bold text-indigo-100">
									Skills
								</div>
								<div
									class="grid grid-cols-1 md:grid-cols-2 gap-y-2 text-slate-400"
								>
									<div
										v-for="skill in master.skills"
										class=""
									>
										<span
											class="font-mono inline-block w-[48px] px-1 py-px mr-2 text-sm text-right text-white/90 bg-green-600 rounded"
											>{{ skill.value }}</span
										>
										<span>{{ skill.name }}</span>
									</div>
								</div>
							</div>
						</div>
					</template>
				</div>
			</div>
		</div>
	</div>
</template>
