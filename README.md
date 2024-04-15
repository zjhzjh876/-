# -
校园博客系统
#include <stdio.h>  
#include <stdlib.h>  
#include <string.h>  
#include <stdbool.h>  
  
#define MAX_USERS 100  
#define MAX_POSTS 100  
#define MAX_COMMENTS 1000  
#define MAX_USERNAME_LENGTH 50  
#define MAX_TITLE_LENGTH 100  
#define MAX_CONTENT_LENGTH 1000  
  
// 用户名结构体  
typedef struct {  
    char username[MAX_USERNAME_LENGTH];  
} Username;  
  
// 用户结构体  
typedef struct {  
    int id;  
    char username[MAX_USERNAME_LENGTH];  
    // 其他用户信息...  
} User;  
  
// 博客文章结构体  
typedef struct {  
    int id;  
    int author_id;  
    char title[MAX_TITLE_LENGTH];  
    char content[MAX_CONTENT_LENGTH];  
    // 其他文章信息...  
} Post;  
  
// 评论结构体  
typedef struct {  
    int id;  
    int post_id;  
    int user_id;  
    char content[MAX_CONTENT_LENGTH];  
    // 其他评论信息...  
} Comment;  
  
// 用户数组  
User users[MAX_USERS];  
int user_count = 0;  
  
// 博客文章数组  
Post posts[MAX_POSTS];  
int post_count = 0;  
  
// 评论数组  
Comment comments[MAX_COMMENTS];  
int comment_count = 0;  
  
// 点赞数组（二维数组，记录用户对文章的点赞情况）  
bool likes[MAX_USERS][MAX_POSTS] = {false};  
  
// 收藏数组（二维数组，记录用户对文章的收藏情况）  
bool favorites[MAX_USERS][MAX_POSTS] = {false};  
  
// 关注数组（二维数组，记录用户对其他用户的关注情况）  
bool follows[MAX_USERS][MAX_USERS] = {false};  
  
// 函数声明  
void add_user(const char* username);  
User* get_user_by_id(int id);  
User* get_user_by_username(const char* username);  
void add_post(const char* title, const char* content, int author_id);  
Post* get_post_by_id(int id);  
void like_post(int user_id, int post_id);  
void unlike_post(int user_id, int post_id);  
void favorite_post(int user_id, int post_id);  
void unfavorite_post(int user_id, int post_id);  
void add_comment(int user_id, int post_id, const char* content);  
void follow_user(int user_id, int target_user_id);  
void unfollow_user(int user_id, int target_user_id);  
User* find_user(const char* username);  
  
// 主函数  
int main() {  
    // 添加用户和文章（这里省略详细逻辑）  
    add_user("Alice");  
    add_user("Bob");  
    add_post("My First Blog", "This is my first blog post.", 1); // 假设Alice是作者  
  
    // 点赞功能演示  
    like_post(2, 1); // Bob点赞了Alice的文章  
    printf("Bob liked Alice's post.\n");  
    unlike_post(2, 1); // Bob取消点赞  
    printf("Bob unliked Alice's post.\n");  
  
    // 收藏功能演示  
    favorite_post(2, 1); // Bob收藏了Alice的文章  
    printf("Bob favorited Alice's post.\n");  
    unfavorite_post(2, 1); // Bob取消收藏  
    printf("Bob unfavorited Alice's post.\n");  
  
    // 评论功能演示  
    add_comment(2, 1, "Great post!"); // Bob对Alice的文章进行了评论  
    printf("Bob commented on Alice's post.\n");  
  
    // 关注用户功能演示  
    follow_user(2, 1); // Bob关注了Alice  
    printf("Bob followed Alice.\n");
