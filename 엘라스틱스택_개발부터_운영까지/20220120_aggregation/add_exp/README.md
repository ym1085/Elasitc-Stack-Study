## HyperLogLog++ Algorithm

> HyperLogLog++는 집합 내 중복되지 않는 항목의 개수를 세기 위한 알고리즘으로, 동일한 목적으로 이미 존재  
> 하던 HyperLogLog를 병렬 처리를 통해 개선한 버전이다. 특징으로는 완전히 정확한 값을 반환하지는 않느나  
> 일반적으로 5% 이내의 오차를 보이며, 정밀도를 직접 지정해 오차율을 낮출 수 있다는 점을 들 수 있다. 또한 카디널  
> 리티가 낮은, 즉 중복을 제거한 항목 수가 적은 집합일수록 100%에 가까운 정확성을 보인다. 특히 집계 대상의 크  
> 기가 얼마나 크든 간에 지정한 정밀도 이상의 메모리를 사용하지 않기 때문에 엘라스틱서치와 같이 대용량 데이터  
> 베이스에서 유용한 알고리즘이다
