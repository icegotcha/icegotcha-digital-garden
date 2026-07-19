---
title: Intersection Observer in React
updated: 2026-02-24T16:12:51+07:00
tags:
  - javascript
---
Mostly, I use `IntersectionObserver` to check whether the element is in the viewpoint (the view which is currently display on the browser)

 ```jsx
 import { useEffect, useRef, useState } from 'react'

  
type UseIntersectionObserverOptions = {
    root?: Element | null
    rootMargin?: string
    threshold?: number | number[]
}

  
export function useIntersectionObserver<T extends Element>(
	options?: UseIntersectionObserverOptions,
): [React.RefObject<T>, boolean] {
	const ref = useRef<T>(null)
	const [isIntersecting, setIsIntersecting] = useState(false)
	
	
	useEffect(() => {
		const target = ref.current
		if (!target) return
		
		const observer = new IntersectionObserver(([entry]) => setIsIntersecting(entry.isIntersecting), options)
		observer.observe(target)
	
		return () => {
			observer.disconnect()
		}
	}, [options])
	
	
	return [ref, isIntersecting]

}
 ```


You can use the library: [react-intersection-observer](https://dev.to/producthackers/intersection-observer-using-react-49ko) to check this:

```jsx
import React from "react";
import { useInView } from "react-intersection-observer";

const Component = () => {
  const { ref, inView, entry } = useInView({
    threshold: 0,
  });

  return (
    <div ref={ref}>
      <h2>{`Header inside viewport ${inView}.`}</h2>
    </div>
  );
};
```



More reference: 
https://dev.to/producthackers/intersection-observer-using-react-49ko