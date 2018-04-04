# bm-web Onboarding Tutorial Solutions

*STOP! BEFORE YOU READ THESE SOLUTIONS...*
1. Ask someone on the team who can guide you in the right direction.
2. Read through the docs for the technology you're struggling with.
3. Google it.

If you've exhausted all of those options and are still stuck, use these solutions sparingly. That is, only look at the parts that you absolutely need.

On the other hand, if you feel like you're done with the tutorial, compare your solution with these. If you're confused about anything in the solutions, feel free to ask a team member.

### Button.jsx
```javascript
// @flow

import styled from 'styled-components'

const colors = {
    blue: '#5c9cef',
    white: '#ffffff'
}

const Button = styled.button`
    border-radius: 50px;
    display: inline-block;
    font-size: 16px;
    font-weight: 400;
    letter-spacing: 0.8px;
    padding: 7px 20px;
    text-align: center;
    font-family: 'Montserrat', sans-serif;
    text-transform: uppercase;
    background-color: ${props => props.primary ? colors.blue : colors.white}
    border: solid 2px ${colors.blue};
    color: ${props => props.primary ? colors.white : colors.blue};
    cursor: pointer;
`

export default Button
```

### LogInButton.jsx

```javascript
// @flow

import React from 'react'
import Button from './Button'

// The three types a LogInButton can be. 
// Each type corresponds to different text and click behavior
type ButtonType = 'login' | 'logout' | 'signup'

type PropsType = {
    // If true, shows just the text 'Log In' instead of a button
    plain: boolean,
    isLoggedIn: boolean,
    // If unspecified, button behaves according to isLoggedIn
    override?: ButtonType
}

function LogInButton(props: PropsType): React.Element<*> {

    // Determine the on-click message corresponding to the button's type
    const getClickMessage = (type: ButtonType) => {
        return {
            login: 'Logging you in...',
            logout: 'Logging you out...',
            signup: 'Signing you up...'
        }[type]
    }

    // Determine the button text corresponding to the button's type
    const getDisplayText = (type: ButtonType): string => {
        return {
            login: 'Log In',
            logout: 'Log Out',
            signup: 'Sign Up Now'
        }[type]
    }

    const handleClick = () => {
        // If an override type is provided, determine message from that type,
        // otherwise determine the type from logged-in status and use that type
        // to determine the message
        const message = props.override ?
            getClickMessage(props.override) :
            getClickMessage(props.isLoggedIn ? 'logout' : 'login')

        window.alert(message)
    }

    // If an override type is provided, determine text from that type,
    // otherwise determine the type from logged-in status and use that type
    // to determine the button text
    const displayText = props.override ?
        getDisplayText(props.override) :
        getDisplayText(props.isLoggedIn ? 'logout' : 'login')

    return (
        <Button primary onClick={handleClick}>
            {displayText}
        </Button>
    )
}

// Declares the default values for props that may not be provided by the composing component
LogInButton.defaultProps = {
    plain: false
    // e.g. if the composing component doesn't specify that it's a plain LogInButton, we default the value of `plain` to false rather than letting it be `undefined`
}

export default LogInButton
```