import pygame
import sys

def main():
    # Initialize all imported pygame modules
    pygame.init()

    # Define constants for window size
    SCREEN_WIDTH = 800
    SCREEN_HEIGHT = 600
    
    # Define colors using RGB tuples
    # Dark blue background: R=20, G=20, B=40
    DARK_BLUE = (20, 20, 40)
    # White color for the alien sprite
    WHITE = (255, 255, 255)
    
    # Create the window display surface
    screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
    
    # Set the title of the window
    pygame.display.set_caption("Pixel Art Character")
  
    # Define a 16x16 Space Invader style alien using a list of strings
    # '1' represents an active pixel (white), '0' represents an empty pixel (transparent)
    alien_pixel_data = [
        "0000011111100000",
        "0000111111110000",
        "0001111111111000",
        "0011100110011100",
        "0011111111111100",
        "0001111111111000",
        "0000100000010000",
        "0001100000011000",
        "0011110000111100",
        "0111111001111110",
        "0110011111100110",
        "0110011111100110",
        "0110001111000110",
        "0011000000001100",
        "0001100000011000",
        "0000000000000000"
    ]
    
    # Create a 16x16 surface to draw the raw pixel art on.
    # We use SRCALPHA to support transparency if we wanted to add it,
    # though here '0' simply skips drawing to let the screen background show.
    sprite_surface = pygame.Surface((16, 16), pygame.SRCALPHA)
    
    # Iterate through the rows and columns of the pixel data array
    for y, row in enumerate(alien_pixel_data):
        for x, pixel in enumerate(row):
            if pixel == '1':
                # Set the pixel on the surface to white
                sprite_surface.set_at((x, y), WHITE)

    # Scale the 16x16 sprite up so it's clearly visible. Let's scale it by 10x.
    scale_factor = 10
    scaled_size = (16 * scale_factor, 16 * scale_factor)
    # Using pygame.transform.scale to enlarge the surface
    character_surface = pygame.transform.scale(sprite_surface, scaled_size)
    
    # Calculate the rectangle to center the scaled character on the screen
    character_rect = character_surface.get_rect(center=(SCREEN_WIDTH // 2, SCREEN_HEIGHT // 2))

    # Variable to keep the main loop running
    running = True

    # The main game loop handles events, updates state, and draws the screen
    while running:
        # Check for events in the event queue
        for event in pygame.event.get():
            # If the user clicks the 'X' button, stop the loop
            if event.type == pygame.QUIT:
                running = False

        # Fill the entire screen surface with the dark blue background
        screen.fill(DARK_BLUE)
        
        # Blit (draw) the character surface onto the screen at the calculated center position
        screen.blit(character_surface, character_rect)

        # Flip the display to update the window with the new drawings
        pygame.display.flip()

    # Uninitialize pygame and exit the system
    pygame.quit()
    sys.exit()

if __name__ == "__main__":
    main()
