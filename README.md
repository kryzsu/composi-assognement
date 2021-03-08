# Composite

A _RobotPart_-ok (számításigényes robot részek taszkjai) névterekbe (_namespace_) vannak hierarchikusan rendezve. 
Egy névtérben lehetnek _RobotPart_ és újabb névterek is.

Csak a _RobotPart_ van valójában komplexitás értéke, ami megmutatja, hogy mennyore bonyolult a számítás.

## TreeNode
A _TreeNode_-nek interfésznek a szokásos _addChild_, _getChildCount_, _removeChild_ műveletei vannak,
amelyek bíztosítják a fa kiépítését.

Ha egy kliensnek szüksége van egy részfában levő levelek (RobotPart) komplexitásának az értékére, akkor ezt meg kell 
határozni (pl.: egy grafikus alkalmazásban drag and droppal áthúzzuk a részfát egy adott node-ra zöld ha mehet, piros ha nem.)

Azért, hogy ne kelljen a kliens oldalon végigjárni a fát (a kliens ne is tudja, hogy fában tároljuk)
kompozit mintát használunk.

## AbstractComponent
Legyen egy _AbstractComponent_ interfész, ami lehetővé teszi a két különböző komponens azonos viselkedését.

```java
  interface AbstractComponent {
    int getComplexity();
    int getCount();
    int getRobotPartCount();
    int getNamespaceCount();
  }
```
	
Mind a _RobotPart_, mind a _Namespace_ implementálja az előbbi interfészt értelem szerűen.

## RobotPart
A _RobotPart_ esetén konstruktorban megkapja a komplexitást, amit eltárol egy _final_ attribútumban.
Implementálja az _AbstractComponent_ interfészt.
* A _getComplexity_ vissza adja a komplexitást.
* A _getRobotPartCount_ 1 ad vissza.
* A _getNamespaceCount_ 0 ad vissza.
* A _getCount_ 1 ad vissza.

## Namespace
Implementálja a _TreeNode_ és az _AbstractComponent_ interfészeket értelem szerűen. Az _AbstractComponent_ metódusainak implementálásánál használj ciklust, összegezd a gyerek komponensek megfelelő metódusát!
* A _Namespace_ esetén a komplexitást a gyerek elemeinek a komplexitás összege adja.
* A _getNamespaceCount_ a gyerek komponensek _getNamespaceCount_-jainkaösszegét + 1-et ad vissza.
* A _getRobotPartCount_ a gyerek komponensek _getRobotPartCount_-jainka összegét adja vissza.
* A _getCount_ a gyerek komponensek _getCount_-jainak összegét + 1-et.
