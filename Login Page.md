# Cypress-Prac
describe('Login Page', () => {
  beforeEach(() => {
    // Visit the login page before each test
    cy.visit('/login')
  })

  it('should display the login form', () => {
    // Verify that the login form elements are present
    cy.get('form').should('be.visible')
    cy.get('input[name="username"]').should('be.visible')
    cy.get('input[name="password"]').should('be.visible')
    cy.get('button[type="submit"]').should('be.visible')
  })

  it('should allow a user to login with valid credentials', () => {
    // Fill in the login form
    cy.get('input[name="username"]').type('myusername')
    cy.get('input[name="password"]').type('mypassword')

    // Submit the form
    cy.get('form').submit()

    // Verify that the user is logged in
    cy.url().should('include', '/dashboard')
    cy.get('h1').should('contain', 'Welcome')
    cy.get('.user-profile').should('be.visible')
  })

  it('should display an error message for invalid login credentials', () => {
    // Fill in the login form with invalid credentials
    cy.get('input[name="username"]').type('invalidusername')
    cy.get('input[name="password"]').type('invalidpassword')

    // Submit the form
    cy.get('form').submit()

    // Verify that an error message is displayed
    cy.get('.error-message').should('be.visible')
  })
})
