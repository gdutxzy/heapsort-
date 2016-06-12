//# heapsort-
//heapsort code in swift



// 堆排序



func leftNodeIndex(heap:(Int)) -> Int{
    return heap*2+1;
}
func rightNodeIndex(heap:(Int)) ->Int{
    return leftNodeIndex(heap)+1;
}
/// 递归方式保持最大根特性
func maxHeapifyRecurrence(inout arry:[Int], index : Int, heapLenght : Int){
    let l = leftNodeIndex(index)
    let r = rightNodeIndex(index)
    var largest = 0;
    if l <= heapLenght-1 && arry[l] > arry[index]{
        largest = l
    }else{
        largest = index
    }
    if r <= heapLenght-1 && arry[r] > arry[largest]{
        largest = r
    }
    if largest != index {
        arry[index] = arry[index]^arry[largest]
        arry[largest] = arry[index]^arry[largest]
        arry[index] = arry[index]^arry[largest]
        maxHeapifyRecurrence(&arry, index: largest, heapLenght: heapLenght)
    }
    
    
}


/// 建立最大堆
func buildMaxHeapRecurrence(inout arry:[Int],heapLenght:Int){
    for var i = heapLenght/2-1 ; i >= 0 ; i-- {
        maxHeapifyRecurrence(&arry, index: i, heapLenght: heapLenght)
    }
    
}

/// 将堆转化成数组顺序
func heapSortUseRecurrence(inout arry:[Int]){
    buildMaxHeapRecurrence(&arry, heapLenght: arry.count)
    for var i = arry.count-1 ; i > 0; i-- {
        arry[i] = arry[0]^arry[i]
        arry[0] = arry[0]^arry[i]
        arry[i] = arry[0]^arry[i]
        maxHeapifyRecurrence(&arry, index: 0, heapLenght: i)
    }
}



var orignArry = [6,1,5,0,12,567,123,126,78,890,232,23]
heapSortUseRecurrence(&orignArry)



/// 循环方式保持最大根特性
func maxHeapifycirculate(inout arry:[Int], index : Int, heapLenght : Int){
    var nChild = 0
    for var i = index ; 2*i+1 < heapLenght; i=nChild{
        nChild=2*i+1;
        if nChild < heapLenght-1 && arry[nChild+1]>arry[nChild] {
            ++nChild
        }
        if arry[i] < arry[nChild] {
            arry[i] = arry[nChild]^arry[i]
            arry[nChild] = arry[nChild]^arry[i]
            arry[i] = arry[nChild]^arry[i]
        }else{
            break
        }
    }
}
func buildMaxHeapcirculate(inout arry:[Int],heapLenght:Int){
    for var i = heapLenght/2-1 ; i >= 0 ; i-- {
        maxHeapifycirculate(&arry, index: i, heapLenght: heapLenght)
    }
    
}
func heapSortUseCirculate(inout arry:[Int]){
    buildMaxHeapcirculate(&arry, heapLenght: arry.count)
    for var i = arry.count-1 ; i > 0; i-- {
        arry[i] = arry[0]^arry[i]
        arry[0] = arry[0]^arry[i]
        arry[i] = arry[0]^arry[i]
        maxHeapifycirculate(&arry, index: 0, heapLenght: i)
    }
}

heapSortUseCirculate(&orignArry)
print(orignArry)
