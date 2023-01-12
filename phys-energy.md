# Physics Energy Calculator

<br>

## Create an object

<form id="obj-create-form">
    <!-- Name of object -->
    <label for="name-input">Name of Object</label><br>
    <input type="text" id="name-input" name="Name"><br>
    <!-- Mass of object -->
    <label for="mass-input">Mass of Object</label><br>
    <input type="text" id="mass-input" name="Mass"><br>
    <button type="submit" id="obj-create-submit">Create Object</button>
</form>

<br>

## KE Calculator

<form id="KE-form">
    <!-- Dropdown to select object -->
    <label for="object-selector"> Select an Object </label><br>
    <select id="object-selector" name="object-selector">
        <option value="{object.ID}"> {object1.name} </option>
        <option value="{object.ID}"> {object2.name} </option>
    </select><br>
    <!-- Velocity of object -->
    <label for="v-input">Velocity Value</label><br>
    <input type="text" id="v-input" name="V"><br>
    <button type="submit" id="KE-submit">Calculate</button>
</form> 

<br>

## PE Gravity Calculator

<form id="PEG-form">
    <!-- Dropdown to select object -->
    <label for="object-selector"> Select an Object </label><br>
    <select id="object-selector" name="object-selector">
        <option value="{object.ID}"> {object1.name} </option>
        <option value="{object.ID}"> {object2.name} </option>
    </select><br>
    <!-- Height of object -->
    <label for="h-input"> Height Value</label><br>
    <input type="text" id="h-input" name="H"><br>
    <!-- Gravity value -->
    <label for="g-input"> G Value</label><br>
    <input type="text" id="g-input" name="G"><br>
    <button type="submit" id="PEG-submit">Calculate</button>
</form> 

