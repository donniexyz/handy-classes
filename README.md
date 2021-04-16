# handy-classes

## Lombok

### CloseableTemporaryVariable

Extending lombok @Cleanup annotation to store a variable and pass it to consumer function upon returning.

#### Example of use case:
1. How to add a method call before returning from a method on java without writing try{} finally{} boilerplate?
2. How to reset value before returning from a method on java without writing try{} finally{} boilerplate?
3. How to push a value and pop it before returning from a method on java without writing try{} finally{} boilerplate?

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
