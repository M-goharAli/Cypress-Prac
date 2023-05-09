# Cypress-Prac
describe('Add to Cart', () => {
  beforeEach(() => {
    // Visit the product page before each test
    cy.visit('/product/123') // Replace "/product/123" with the actual URL of your product page
  })

  it('should add a product to the cart', () => {
    // Click on the "Add to Cart" button
    cy.get('.add-to-cart-button').click()

    // Verify that the product is added to the cart
    cy.get('.cart-item').should('have.length', 1) // Assuming the cart items have a class of ".cart-item"
    cy.get('.cart-total').should('contain', '1 item') // Assuming the cart total element has a class of ".cart-total"
  })

  it('should update the cart quantity when adding multiple products', () => {
    // Click on the "Add to Cart" button multiple times
    cy.get('.add-to-cart-button').click().click().click()

    // Verify that the product quantity is updated in the cart
    cy.get('.cart-item').should('have.length', 3)
    cy.get('.cart-total').should('contain', '3 items')
  })

  it('should remove a product from the cart', () => {
    // Add a product to the cart
    cy.get('.add-to-cart-button').click()

    // Click on the "Remove" button for the product in the cart
    cy.get('.cart-item').first().find('.remove-button').click() // Assuming the remove button has a class of ".remove-button"

    // Verify that the product is removed from the cart
    cy.get('.cart-item').should('have.length', 0)
    cy.get('.cart-total').should('contain', '0 items')
  })
})
