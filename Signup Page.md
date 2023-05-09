# Cypress-Prac

describe('Signup Page', () => {
  beforeEach(() => {
    // Visit the signup page before each test
    cy.visit('/signup')
  })

  it('should display the signup form', () => {
    // Verify that the signup form elements are present
    cy.get('form').should('be.visible')
    cy.get('input[name="username"]').should('be.visible')
    cy.get('input[name="email"]').should('be.visible')
    cy.get('input[name="password"]').should('be.visible')
    cy.get('input[name="confirmPassword"]').should('be.visible')
    cy.get('button[type="submit"]').should('be.visible')
  })

  it('should allow a user to signup with valid credentials', () => {
    // Fill in the signup form
    cy.get('input[name="username"]').type('myusername')
    cy.get('input[name="email"]').type('myemail@example.com')
    cy.get('input[name="password"]').type('mypassword')
    cy.get('input[name="confirmPassword"]').type('mypassword')

    // Submit the form
    cy.get('form').submit()

    // Verify that the user is signed up and logged in
    cy.url().should('include', '/dashboard')
    cy.get('h1').should('contain', 'Welcome')
    cy.get('.user-profile').should('be.visible')
  })

  it('should display an error message for invalid signup credentials', () => {
    // Fill in the signup form with invalid credentials
    cy.get('input[name="username"]').type('existingusername')
    cy.get('input[name="email"]').type('existingemail@example.com')
    cy.get('input[name="password"]').type('mypassword')
    cy.get('input[name="confirmPassword"]').type('mypassword')

    // Submit the form
    cy.get('form').submit()

    // Verify that an error message is displayed
    cy.get('.error-message').should('be.visible')
  })
})
