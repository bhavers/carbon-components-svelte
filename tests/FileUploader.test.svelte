<script lang="ts">
  import {
    FileUploaderButton,
    FileUploader,
    FileUploaderDropContainer,
    FileUploaderItem,
    FileUploaderSkeleton,
  } from "carbon-components-svelte";
  import type { FileUploaderProps } from "carbon-components-svelte/FileUploader/FileUploader.svelte";

  let fileUploader: FileUploader;
  let files: FileUploaderProps["files"] = [];

  $: {
    // @ts-expect-error
    files[0] = null;
  }

  $: fileUploader?.clearFiles();
</script>

<FileUploaderButton
  kind="tertiary"
  size="xl"
  labelText="Add files"
  on:change={(e) => {
    console.log(e.detail); // File[]
  }}
/>

<FileUploader
  kind="danger-ghost"
  size="lg"
  bind:this={fileUploader}
  multiple
  labelTitle="Upload files"
  buttonLabel="Add files"
  labelDescription="Only JPEG files are accepted."
  accept={[".jpg", ".jpeg"]}
  status="complete"
  bind:files
  on:add={(e) => {
    console.log(e.detail); // File[]
  }}
  on:remove={(e) => {
    console.log(e.detail); // File[]
  }}
  on:change={(e) => {
    console.log(e.detail); // File[]
  }}
/>

<FileUploaderItem name="README.md" status="uploading" />

<FileUploaderItem name="README.md" status="complete" />

<FileUploaderItem invalid name="README.md" status="edit" />

<FileUploaderDropContainer
  labelText="Drag and drop files here or click to upload"
  multiple
/>

<FileUploaderSkeleton />
