function test() {
  path = '/Folder1/Folder2/Folder3/';
  writePlain(makeFolder(path), 'test1.txt', 'hogehoge');
  writePlain(getFolder(path), 'test1.txt', 'hogehoge');
}

/* フォルダが存在すれば、そのFolderオブジェクトを返す(存在しない場合はnull) */
function getFolderByPath(path, currentFolder) {
  return getFolderCore(path, currentFolder, false);
}

/* フォルダを作成し、そのFolderオブジェクトを返す */
function makeFolder(path, currentFolder) {
  return getFolderCore(path, currentFolder, true);
}

/* コアメソッド */
function getFolderCore(path, currentFolder, mkFolderFlg) {
  var pathArray = path.replace(/^[/]*|[/]*$/g, '').split('/');
  
  if (currentFolder == null) {
    currentFolder = DriveApp.getRootFolder();
  }
  
  var existFlg = pathArray.every(function(folderName) {
    var continueFlg = true;
    var folderItr = currentFolder.getFoldersByName(folderName);
    
    if (folderItr.hasNext()) {
      currentFolder = folderItr.next();
    } else if (mkFolderFlg) {
      currentFolder = currentFolder.createFolder(folderName);
    } else {
      continueFlg = false;
    }
    return continueFlg;
  });
  if (existFlg) {
    return currentFolder;
  }
  return null;
}

/* ファイルを作成(上書き)する */
function writePlain(folder, fileName, text) {
  // ファイルを取得(同じ名前を持つファイルがフォルダ内に複数存在しない事前提)
  var fileItr = folder.getFilesByName(fileName);
  if (fileItr.hasNext()) folder.removeFile(fileItr.next());
  return folder.createFile(fileName, text);
}
