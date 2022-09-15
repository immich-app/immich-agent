<script lang="ts">
  import {
    readBinaryFile,
    writeTextFile,
    readDir,
    Dir,
  } from "@tauri-apps/api/fs";
  import { open, save } from "@tauri-apps/api/dialog";

  const openFolderSelector = async () => {
    const path = await open({
      title: "Select a folder to upload",
      defaultPath: null,
      multiple: false,
      directory: true,
    });

    if (path && typeof path == "string") {
      const entries = await readDir(path, {
        recursive: true,
      });

      for (const entry of entries) {
        console.log("Top level entry", entry);
        if (entry.children) {
          console.log(entry.children);
        }
      }
    }
  };
</script>

<main class="grid place-items-center place-content-center">
  <h1>Immich Agent</h1>
  <div>
    <button class="border rounded-md px-4 py-2" on:click={openFolderSelector}
      >Chose watch folder</button
    >
  </div>
</main>
