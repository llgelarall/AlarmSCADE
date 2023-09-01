{
 "cells": [
  {
   "cell_type": "markdown",
   "id": "baebc205-b3d2-410d-85b1-98e6746e0f7f",
   "metadata": {},
   "source": [
    "# Implementation of Alarm System in SCADE\n",
    "\n",
    "In this implementation, the Alarm system is situated within the Scade operating environment's AlarmCom operator. The initial state of the system is denoted as `SM1`, and it includes two modes: `Shut` and `OP`.\n",
    "\n",
    "The behavior of the system is governed by the `PressKey` input, which is a boolean value. When `PressKey` is true, it corresponds to the system's start action, and when false, it corresponds to shutting the system. Transitions in this system rely on strong conditions.\n",
    "\n",
    "The key adjustment involves correcting the `PressKey` entry to ensure a transition to the `OP` mode. Additionally, there are two parallel state machines: `Vol` and `Mode`. The `Vol` state machine is responsible for managing two volume levels, 1 and 2, while the `Mode` state machine handles two modes: `on` and `off`.\n",
    "\n",
    "Transition conditions for the modes are established based on inputs `tOn` and `tOff`. When `tOn` is true, the system switches to the \"on\" mode, and `tOff` leads to the \"off\" mode. In the `Vol` state machine, `Inc` leads to `2Vol` when true, and `Dec` leads to `1Vol` when true.\n",
    "\n",
    "It's important to note that changing the mode in one state machine doesn't affect the parallel state machine. Visual aids, such as diagrams and images, help clarify the transitions and states.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "b18703b2-1f3d-4bab-8bcf-1cbd23a47763",
   "metadata": {},
   "source": [
    "\n",
    "<div style=\"text-align:center;\">\n",
    "  <img src=\"Final.png\" alt=\"State Transition Diagram\">\n",
    "</div>"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "2e7276ea-7239-4666-a358-45683825b0cf",
   "metadata": {},
   "source": [
    "## Transitions and Visuals\n",
    "\n",
    "Each transition is associated with a corresponding output, which aids in debugging and analyzing the active state, especially in non-animated modes.\n",
    "\n",
    "## State Changes\n",
    "\n",
    "Based on the provided diagram, transitioning from `OP` mode to `Shut` mode is possible by setting `PressKey` to false and otherwise.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c90ca9f0-25b3-41ce-b8c1-d83c00e6fca7",
   "metadata": {},
   "source": [
    "<div style=\"text-align:center;\">\n",
    "  <img src=\"1.png\" alt=\"State Transition Diagram\">\n",
    "</div>"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a5a44026-8fd1-4e2c-ad5f-78eb5ea208be",
   "metadata": {},
   "source": [
    "## Walkthrough\n",
    "\n",
    "In the `OP` mode, based on the diagram, a transition is made by setting the `PressKey` input (start) to true. This is influenced by the initial mode settings: off for `Mode` and Vol1 for `Vol`. As a result, the `OP` mode becomes active upon entry.\n",
    "\n",
    "\n",
    "\n",
    "\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "5f8d4651-bdf2-40d9-9f39-35be0c15b8f5",
   "metadata": {},
   "source": [
    "<div style=\"text-align:center;\">\n",
    "  <img src=\"tOn.png\" alt=\"pic3\">\n",
    "</div>"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "36e3d600-433d-4a0d-8af9-8345905c2e4b",
   "metadata": {},
   "source": [
    "In another scenario depicted in picture 3, with `tOn` set to true, the `Mode` state machine switches to \"on.\" Simultaneously, the `Vol` state machine remains in `1Vol` mode, and the main machine mode is `OP`."
   ]
  },
  {
   "cell_type": "markdown",
   "id": "a4d2a604-39d3-4afc-8868-47b4ad602ee4",
   "metadata": {},
   "source": [
    "<div style=\"text-align:center;\">\n",
    "  <img src=\"inc.png\" alt=\"pic4\">\n",
    "</div>"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "729b8fc6-f901-4756-b4da-d0c649246930",
   "metadata": {},
   "source": [
    "\n",
    "Image 4 illustrates that by setting `Inc` to true, the `Vol` mode transitions to `2Vol`. Similarly, in picture 5, `Dec` becomes true, following the previous change, leading to a transition to `1Vol`.\n"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "78ed08e6-b221-46c9-96a3-dcf0059a3289",
   "metadata": {},
   "source": [
    "<div style=\"text-align:center;\">\n",
    "  <img src=\"dec.png\" alt=\"pic5\">\n",
    "</div>"
   ]
  },
  {
   "cell_type": "markdown",
   "id": "c23ec997-1ebb-41a7-a1c4-063ea4cb879e",
   "metadata": {},
   "source": [
    "## Conclusion\n",
    "\n",
    "Finally, changing `PressKey` to false causes the main machine (`SM1`) to transition from `OP` mode to `Shut` mode, concluding the scenario smoothly."
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.9.13"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
