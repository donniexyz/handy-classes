# handy-classes

## Lombok

### CloseableTemporaryVariable

Extending lombok @Cleanup annotation to store a variable and pass it to consumer function upon returning.

#### How to use:

     ...
     @Cleanup CloseableTemporaryVariable<List> temporaryVariable = new CloseableTemporaryVariable<>(trxGroup.getChilds(), trxGroup::setChilds);
     trxGroup.setChilds(null);
     ...

#### Translated into java:

     ...
     CloseableTemporaryVariable<List> temporaryVariable = new CloseableTemporaryVariable<>(trxGroup.getChilds(), trxGroup::setChilds);
     // meaning temporaryVariable.data = trxGroup.getChilds()

     try {
         trxGroup.setChilds(null);
         ...
     } finally {
         if (temporaryVariable != null)
             temporaryVariable.close();  // meaning trxGroup.setChilds(temporaryVariable.data)
     }
