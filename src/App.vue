<script setup>
import {ref} from "vue";

window.onload = function() {
  // передача идентификатора родительского элемента
  fileTree('file-tree');
};

// если работать в js, то применяется var, если в самом App.vue, то используем const



function fileTree(elementId) {
  // наш селектор
  NodeList.prototype.has = function (selector) {
    // возвращаем наш массив
    return Array.from(this).filter(e => e.querySelector(selector))
  };
  const element = document.getElementById(elementId)
  // создаем класс-лист для работы со списком
  element.classList.add('file-list')

  const liElementsInsideUl = element.querySelectorAll('li');
  liElementsInsideUl.has('ul').forEach(li => {
    li.classList.add('folder-root');
    li.classList.add('closed');
    const spanFolderElementInsideLi = li.querySelectorAll('span.folder-name');
    spanFolderElementInsideLi.forEach(span => {
      if (span.parentNode.nodeName === 'LI') {
        span.onclick = function (e) {
          span.parentNode.classList.toggle('open');
        };
      }
    });
  });
}



function editFileName(id) {
  let nameFile = document.getElementById(id);
  const newNameFile = prompt('Введите новое название папки/файла', nameFile.innerText);
  if (newNameFile) {
    nameFile.innerText = newNameFile;
  }
}
function deleteFileName(id) {
  const deleteButton = document.getElementById(id);
  if (deleteButton) {
    deleteButton.parentNode.removeChild(deleteButton);
  }
}

</script>

<template>
  <div>
    <div class="container">
      <div class="directive">
        <ul id="file-tree" class="file-tree">
          <li id="replace-1">
            <span id="replaced-1" class="folder-name">Dir 1</span>
            <button id="edit" class="edit" @click="editFileName('replaced-1')">
              <img src="../src/assets/edit.svg">
            </button>
            <button id="delete" class="delete" @click="deleteFileName('replaced-1')">
              <img src="../src/assets/delete.svg">
            </button>
            <ul>
              <li id="replace-1-1">
                <span id="replaced-1-1" class="folder-name">Dir 1-1</span>
                <button id="edit" class="edit" @click="editFileName('replaced-1-1')">
                  <img src="../src/assets/edit.svg">
                </button>
                <button id="delete" class="delete" @click="deleteFileName('replace-1-1')">
                  <img src="../src/assets/delete.svg">
                </button>
                <ul>
                  <li id="replace-1-1-1">
                    <p id="replaced-1-1-1">file 1-1-1</p>
                    <button id="edit" class="edit" @click="editFileName('replaced-1-1-1')">
                      <img src="../src/assets/edit.svg">
                    </button>
                    <button id="delete" class="delete" @click="deleteFileName('replaced-1-1-1')">
                      <img src="../src/assets/delete.svg">
                    </button>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
          <li>
            <span id="replaced-2" class="folder-name">Dir 2</span>
            <button id="edit" class="edit" @click="editFileName('replaced-2')">
              <img src="../src/assets/edit.svg">
            </button>
            <button id="delete" class="delete" @click="deleteFileName('replaced-2')">
              <img src="../src/assets/delete.svg">
            </button>
            <ul>
              <li>
                <p id="replaced-2-1" class="folder-name">Dir 2-1</p>
                <button id="edit" class="edit" @click="editFileName('replaced-2-1')">
                  <img src="../src/assets/edit.svg">
                </button>
                <button id="delete" class="delete" @click="deleteFileName('replaced-2-1')">
                  <img src="../src/assets/delete.svg">
                </button>
                <ul>
                </ul>
              </li>
              <li>
                <p id="replaced-2-2">file 2-2</p>
                <button id="edit" class="edit" @click="editFileName('replaced-2-2')">
                  <img src="../src/assets/edit.svg">
                </button>
                <button id="delete" class="delete" @click="deleteFileName('replaced-2-2')">
                  <img src="../src/assets/delete.svg">
                </button>
              </li>
            </ul>
          </li>
          <li>
            <p id="replaced-2.1">file 2</p>
            <button id="edit" class="edit" @click="editFileName('replaced-2.1')">
              <img src="../src/assets/edit.svg">
            </button>
            <button id="delete" class="delete" @click="deleteFileName('replaced-2.1')">
              <img src="../src/assets/delete.svg">
            </button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style>
@import "style.css";
</style>
