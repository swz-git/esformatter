<script>
  import esbuild from "esbuild-wasm";
  esbuild.initialize({
    wasmURL: "https://unpkg.com/esbuild-wasm/esbuild.wasm",
  });
  async function format() {
    let input = document.getElementById("input").value;
    let result = await esbuild.transform(input, {
      minifyWhitespace: document.getElementById("whitespace").checked,
      minifyIdentifiers: document.getElementById("identifiers").checked,
      minifySyntax: document.getElementById("syntax").checked,
    });
    document.getElementById("output").innerHTML = result.code;
  }
</script>

<main>
  <header>
    <h1>esformatter</h1>
  </header>
  <div class="splitter">
    <textarea name="input" id="input" on:keyup={format} />
    <textarea name="output" id="output" disabled />
  </div>
  <footer>
    <div class="checkwrapper">
      <input type="checkbox" id="whitespace" on:change={format} />
      <p>Minify whitespace</p>
    </div>
    <div class="checkwrapper">
      <input type="checkbox" id="identifiers" on:change={format} />
      <p>Minify identifiers</p>
    </div>
    <div class="checkwrapper">
      <input type="checkbox" id="syntax" on:change={format} />
      <p>Minify syntax</p>
    </div>
  </footer>
</main>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  html,
  body,
  main {
    display: flex;
    height: 100%;
    width: 100%;
    flex-direction: column;
  }
  main {
    background-color: #323232;
    color: white;
    flex: 1;
  }
  header {
    width: 100%;
    text-align: center;
  }
  .splitter {
    display: flex;
    flex-direction: row;
    flex: 1;
    width: 100%;
    gap: 0.5rem;
  }
  textarea {
    background-color: white;
    resize: none;
    flex: 1;
  }
  footer {
    display: flex;
    justify-content: space-around;
  }
  .checkwrapper {
    display: flex;
  }
  button {
    font-size: 1.3rem;
    margin: 0.2rem;
    padding: 0.2rem 0.4rem;
    border: none;
    background-color: #0077ff;
  }
  button:active {
    background-color: #0044ff;
  }
</style>
