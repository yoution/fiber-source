

// render
performWork
invokeGuardedCallback workLoop
    performUnitOfWork
      beginWork
        fiber.tag
          HostRoot
            workInProgress.effectTag
            workInProgress.child
              childType
                REACT_ELEMENT_TYPE:
                REACT_COURTINE_TYPE:
                REACT_YIELD_TYPE:
                REACT_PORTAL_TYPE:
            childFiber.return = workInProgress
          ClassComponent
            constructClassInstance
            workInProgress.stateNode = instance
            componentWillMount
            childFiber.return = workInProgress.render
          HostComponent:
            workInProgress.child = null
    completeUnitWork
      completeWork
        HostComponent:
          document.createElement 
          appendChild
          workInProgress.stateNode = domNode
          returnFiber.firstEffect = workInProgress
          returnFiber.lastEffect = workInProgress
        ClassComponent:
          return 
        HostRoot:
          return 
        HostText:
        CORoutineComponent:
        YieldComponent:
        Fragment:
        HostPortal:
        IndeterminateComponent:

    commitAllWork
      resetTextContent
      comitDetachRef
      effectTag:  nextEffect
        Placement:
          appendChildToContainer
        PlacementAndUpdate:
        Update:
          ClassComponent:
            return;
          HostComponent:
          HostText:
          HostRoot:
          HostPortal
        Deletion:




    
invokeGuardedCallback commitAllLifeCycles
  whild(effectTag)
    fiber.tag:
      ClassComponent:
      instant.componentDidMount
      or instant.componetDidUpdate

    

// update
performWork
invokeGuardedCallback workLoop
    performUnitOfWork
      beginWork
        fiber.tag
          HostRoot
            workInProgress.effectTag
            workInProgress.child
              childType
                REACT_ELEMENT_TYPE:
                REACT_COURTINE_TYPE:
                REACT_YIELD_TYPE:
                REACT_PORTAL_TYPE:
            childFiber.return = workInProgress
          ClassComponent
            componentWillReceiveProps
            shouldComponentUpdate
            componentWillUpdate
            render
          HostComponent:
            workInProgress.child = null
    completeUnitWork
      completeWork
        HostComponent:
          document.createElement 
          appendChild
          workInProgress.stateNode = domNode
          returnFiber.firstEffect = workInProgress
          returnFiber.lastEffect = workInProgress
        ClassComponent:
          return 
        HostRoot:
          return 
        HostText:
        CORoutineComponent:
        YieldComponent:
        Fragment:
        HostPortal:
        IndeterminateComponent:

    commitAllWork
      resetTextContent
      comitDetachRef
      effectTag:  nextEffect
        Placement:
          appendChildToContainer
        PlacementAndUpdate:
        Update:
          ClassComponent:
            return;
          HostComponent:
          HostText:
          HostRoot:
          HostPortal
        Deletion:




    
invokeGuardedCallback commitAllLifeCycles
  whild(effectTag)
    fiber.tag:
      ClassComponent:
      instant.componentDidMount
      or instant.componetDidUpdate

    


invokeGuardedCallback performWorkCatchBlock
invokeGuardedCallback commitAllHostEffects
invokeGuardedCallback performWorkCatchBlock
invokeGuardedCallback commitAllHostEffects
