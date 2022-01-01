<script>
  import esbuild from "esbuild-wasm";
  esbuild.initialize({
    wasmURL: "https://unpkg.com/esbuild-wasm@0.14.7/esbuild.wasm",
  });
  let error = false;
  async function format() {
    let input = document.getElementById("input").value;
    esbuild
      .transform(input, {
        minifyWhitespace: document.getElementById("whitespace").checked,
        minifyIdentifiers: document.getElementById("identifiers").checked,
        minifySyntax: document.getElementById("syntax").checked,
      })
      .then((result) => {
        error = false;
        document.getElementById("output").innerHTML = result.code;
        // console.log(result.code);
      })
      .catch((e) => {
        // console.log(e);
        error = true;
      });
  }
</script>

<main>
  <header>
    <h1>esformatter</h1>
  </header>
  <div class="splitter">
    <div class="codewrapper">
      <textarea name="input" id="input" on:keyup={format} />
    </div>
    <div class="codewrapper">
      <textarea
        name="output"
        id="output"
        class={error ? "error" : "noerror"}
        disabled
      />
    </div>
  </div>
  <div class="options">
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
  </div>
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
  .codewrapper {
    flex: 1;
    display: flex;
  }
  textarea {
    background-color: white;
    resize: none;
    flex: 1;
  }
  .options {
    display: flex;
    justify-content: center;
    gap: 1rem;
  }
  .checkwrapper {
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .error {
    color: red;
  }
</style>
