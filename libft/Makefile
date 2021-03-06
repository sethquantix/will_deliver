# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Makefile libft                                     :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: hmartzol <hmartzol@student.42.fr>          +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2016/01/30 23:15:42 by hmartzol          #+#    #+#              #
#    Updated: 2016/03/08 21:41:25 by hmartzol         ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

NAME =			libft.a

SRCDIR =		src
OBJDIR =		OBJ
INCDIR =		includes

LIBDIR =		
LIBNAME =		

INCLUDES =		libft
ITEMS =			ft_memset ft_bzero ft_memcpy ft_memccpy ft_memmove ft_memchr \
				ft_memcmp ft_strlen ft_strdup ft_strcpy ft_strncpy ft_strcat \
				ft_strncat ft_strlcat ft_strchr ft_strrchr ft_strstr \
				ft_strnstr ft_strcmp ft_strncmp ft_atoi ft_isalpha ft_isdigit \
				ft_isalnum ft_isascii ft_isprint ft_toupper ft_tolower \
				ft_memalloc ft_memdel ft_strnew ft_strdel ft_strclr \
				ft_striter ft_striteri ft_strmap ft_strmapi ft_strequ \
				ft_strnequ ft_strsub ft_strjoin ft_strtrim ft_strsplit \
				ft_itoa ft_putchar ft_putstr ft_putendl ft_putnbr \
				ft_putchar_fd ft_putstr_fd ft_putendl_fd ft_putnbr_fd \
				ft_lstnew ft_lstdelone ft_lstdel ft_lstadd ft_lstiter \
				ft_lstmap ft_puttab ft_puttab_fd ft_putlist ft_putlist_fd \
				ft_lstappend ft_isspace ft_strcntc ft_readfile ft_ptinit \
				ft_ptnew ft_sin ft_cos ft_tan ft_point ft_point3d

CC =			gcc
FLAGS =			-Wall -Wextra -Werror

INCLUDE =		-I$(INCDIR)/
LIBS =			
LIBS_LINUX =	
LIBS_IOS =		

OS =			$(shell uname)
OBJ =			$(patsubst %, $(OBJDIR)/%.o, $(ITEMS))

ifeq ($(OS), Darwin)
	LIB = $(LIBS) $(LIBS_IOS)
else ifeq ($(OS), Linux)
	LIB = $(LIBS) $(LIBS_LINUX)
endif
OBJMODE =
ifneq ($(OBJDIR), .)
ifneq ($(OBJDIR), $(SRCDIR))
ifneq ($(OBJDIR), $(INCDIR))
OBJMODE = TRUE
endif
endif
endif

.PHONY: all
all: $(NAME)

ifeq ($(suffix $(NAME)), .a)
$(NAME): auteur $(OBJDIR) $(OBJ)
	@echo "Linking objects together into $(NAME)..."
	@ar rc $@ $(OBJ)
	@echo "Linking succesfull, starting ranlib..."
	@ranlib $@
	@echo "ranlib succesfull"
else
ifdef LIBNAME
ifdef LIBDIR
$(NAME): $(LIBDIR)/$(LIBNAME) auteur $(OBJDIR) $(OBJ)
	@echo "Compiling the executable $(NAME)..."
	@$(CC) $(FLAGS) $(INCLUDE) $(LIB) $(OBJ) $(LIBDIR)/$(LIBNAME) -o $@
	@echo "Compiling succesfull"
else
$(NAME): $(LIBNAME) auteur $(OBJDIR) $(OBJ)
	@echo "Compiling the executable $(NAME)..."
	@$(CC) $(FLAGS) $(INCLUDE) $(LIB) $(OBJ) $(LIBNAME) -o $@
	@echo "Compiling succesfull"
endif
else
$(NAME): auteur $(OBJDIR) $(OBJ)
	@echo "Compiling the executable $(NAME)..."
	@$(CC) $(FLAGS) $(INCLUDE) $(LIB) $(OBJ) -o $@
	@echo "Compiling succesfull"
endif
endif

ifdef LIBNAME
ifdef LIBDIR
$(LIBDIR)/$(LIBNAME):
	@echo "Creating sublib $(LIBNAME)..."
	@make re -C $(LIBDIR)/
endif
endif

$(OBJDIR):
ifdef OBJMODE
	@echo "Making temporary object directory: $(OBJDIR)..."
	@mkdir $(OBJDIR)
	@echo "Directory succesfully created"
endif

$(OBJDIR)/%.o: $(SRCDIR)/%.c
	$(CC) $(FLAGS) $(INCLUDE) $(LIBS) -c $< -o $@

.PHONY: clean
clean:
ifdef OBJMODE
	@echo "Removing object directory: $(OBJDIR)..."
	@rm -rf $(OBJDIR)
else
	@echo "Removing objects"
	@rm -f $(patsubst %, $(OBJDIR)/%.o, $(ITEMS))
endif
	@echo "Removing succesfull"
	@echo "Removing swaps and undesirable files..."
	@rm -f $(patsubst %, $(SRCDIR)/%.c~, $(ITEMS))
	@rm -f $(patsubst %, $(SRCDIR)/#%.c#, $(ITEMS))
	@rm -f $(patsubst %, $(SRCDIR)/.%.c.swp, $(ITEMS))
	@rm -f $(patsubst %, $(INCDIR)/%.h~, $(INCLUDES))
	@rm -f $(patsubst %, $(INCDIR)/#%.h#, $(INCLUDES))
	@rm -f $(patsubst %, $(INCDIR)/.%.h.swp, $(INCLUDES))
ifneq ($(INCDIR), .)
	@rm -f $(patsubst %, $(INCDIR)/%, .DS_Store ._.DS_Store)
endif
ifneq ($(SRCDIR), .)
	@rm -f $(patsubst %, $(SRCDIR)/%, .DS_Store ._.DS_Store)
endif
	@rm -f .DS_Store ._.DS_Store
	@echo "Removing succesfull"
ifdef LIBNAME
ifdef LIBDIR
	@echo "Executing clean on sublib: $(LIBNAME)"
	@make -C $(LIBDIR) clean
endif
endif

.PHONY: fclean
fclean: clean
ifeq ($(suffix $(NAME)), .a)
	@echo "Removing library: $(NAME)..."
else
	@echo "Removing executable: $(NAME)..."
endif
	@rm -rf $(NAME)
	@echo "Removing succesfull"
ifdef LIBNAME
ifdef LIBDIR
	@echo "Executing fclean on sublib: $(LIBNAME)"
	@make -C $(LIBDIR) fclean
endif
endif

.PHONY: re
re: fclean all

.PHONY: norm
norm:
	@clear
	@echo "Looking for norm errors in the sources and includes..."
	@norminette $(patsubst %, $(SRCDIR)/%.c, $(ITEMS))
	@norminette $(patsubst %, $(INCDIR)/%.h, $(INCLUDES))

auteur:
	@echo "Creating default auteur file..."
	@echo "hmartzol" > auteur
	@echo "Default auteur file succesfully created"
