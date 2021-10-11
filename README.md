IMHO the best way how to implement responsiveness

how to use:
```
import styled from "styled-components"

export const Box = styled.div`
	color: #393939;
	font-size: 12px;

	${media.greaterThan("large")`
		font-size: 16px;	
	`};
`
```



code:
```
// IPAD     : 768x1024  // 1024x768
// IPAD PRO : 1024x1366 // 1366x1024
export const breakpoints = {
  huge: rem("1366px"),
  large: rem("1024px"),
  medium: rem("768px"),
};

const getSize = (size) => {
  if (breakpoints[size]) {
    return breakpoints[size];
  } else if (parseInt(size)) {
    return size;
  } else {
    return "0";
  }
};

export const media = {
  lessThan:
    (breakpoint: keyof typeof breakpoints) =>
    (literals: TemplateStringsArray, ...args: any[]) =>
      css`
        @media (max-width: ${getSize(breakpoint)}) {
          ${css(literals, ...args)}
        }
      `,

  greaterThan:
    (breakpoint: keyof typeof breakpoints) =>
    (literals: TemplateStringsArray, ...args: any[]) =>
      css`
        @media (min-width: ${getSize(breakpoint)}) {
          ${css(literals, ...args)}
        }
      `,

  between:
    (
      firstBreakpoint: keyof typeof breakpoints,
      secondBreakpoint: keyof typeof breakpoints
    ) =>
    (literals: TemplateStringsArray, ...args: any[]) =>
      css`
        @media (min-width: ${getSize(
            firstBreakpoint
          )}) and (max-width: ${getSize(secondBreakpoint)}) {
          ${css(literals, ...args)}
        }
      `,
};
```
